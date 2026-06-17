# Security Guidelines

> Security practices for this repository — keeping API tokens, credentials, and webhook URLs out of version control.

---

## Before every git push

Run a manual check:
```bash
grep -r "ntn_\|sk-ant-\|Bearer \|hooks.slack.com" workflows/
grep -r "discordapp.com/api/webhooks/[0-9]" workflows/
```
Both commands must return empty output. If not — fix before pushing.

---

## Pre-commit hook

Required in every repo. Install:
```bash
cat > .git/hooks/pre-commit << 'HOOK'
#!/bin/bash

PATTERNS=(
  "ntn_"
  "sk-ant-"
  "discordapp.com/api/webhooks/[0-9]"
  "hooks.slack.com"
  "Bearer [A-Za-z0-9_\-]\{20,\}"
  "api_key.*:.*\"[A-Za-z0-9]\{20,\}"
)

FOUND=0

for pattern in "${PATTERNS[@]}"; do
  MATCHES=$(git diff --cached --name-only | xargs grep -l -E "$pattern" 2>/dev/null)
  if [ -n "$MATCHES" ]; then
    echo "❌ SECURITY: possible secret found (pattern: $pattern)"
    echo "   Files: $MATCHES"
    FOUND=1
  fi
done

if [ $FOUND -eq 1 ]; then
  echo ""
  echo "Commit blocked. Replace secrets with placeholders and try again."
  exit 1
fi

exit 0
HOOK

chmod +x .git/hooks/pre-commit
```

The hook blocks commits when it detects: Notion tokens, Anthropic keys, Discord webhooks, Slack hooks, or generic Bearer tokens.

---

## Exporting workflow JSON from n8n

n8n sometimes embeds credentials directly into the JSON — especially HTTP Request nodes with hardcoded headers. Never rely on memory; always check before committing.

**Standard placeholders:**

| Service | Placeholder |
|---------|-------------|
| Notion | `YOUR_NOTION_TOKEN` |
| Discord | `YOUR_DISCORD_WEBHOOK_URL` |
| Hunter.io | `YOUR_HUNTER_API_KEY` |
| Anthropic | `YOUR_ANTHROPIC_API_KEY` |
| Slack | `YOUR_SLACK_WEBHOOK_URL` |

---

## After a credential leak — procedure

1. **Revoke immediately** — rotate the exposed key before anything else.
2. **Clean Git history:**
```bash
rm -rf .git
git init
git add .
git commit -m "fix: remove exposed credentials"
git remote add origin git@github.com:USER/REPO.git
git push --force origin master
```
3. **Create a new key** and update it in n8n credentials.
4. **Check other services** exposed in the same repo.

---

## Rules

- GitHub secret scanning only detects after the push — by then the secret is already public. Don't rely on it.
- Bots scan GitHub continuously — "nobody will find it" is not protection.
- Never use live credentials when testing against a public repo.
- `.env` files never go into Git — only `.env.example` with placeholders.
