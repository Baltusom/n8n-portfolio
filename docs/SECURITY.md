# Security Guidelines

> Vytvořeno po incidentu 2026-06-04: expozice Notion API tokenu a Discord webhook URL v public GitHub repozitáři.

---

## Před každým git push

Spustit manuální kontrolu:
```bash
grep -r "ntn_\|sk-ant-\|Bearer \|hooks.slack.com" workflows/
grep -r "discordapp.com/api/webhooks/[0-9]" workflows/
```
Oba příkazy musí vrátit prázdný výstup. Pokud ne — opravit před pushem.

---

## Pre-commit hook

Povinný v každém repu. Instalace:
```bash
cat > .git/hooks/pre-commit << 'EOF'
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
EOF

chmod +x .git/hooks/pre-commit
```

Hook blokuje commit při detekci: Notion tokenů, Anthropic keys, Discord webhooků, Slack hooků, obecných Bearer tokenů.

---

## Export workflow JSON z n8n

n8n někdy vloží credentials přímo do JSON — zejména HTTP Request node s hardcoded headers. Nikdy nespoléhat na paměť, vždy zkontrolovat před commitem.

**Standardní placeholdery:**

| Service | Placeholder |
|---------|-------------|
| Notion | `YOUR_NOTION_TOKEN` |
| Discord | `YOUR_DISCORD_WEBHOOK_URL` |
| Hunter.io | `YOUR_HUNTER_API_KEY` |
| Anthropic | `YOUR_ANTHROPIC_API_KEY` |
| Slack | `YOUR_SLACK_WEBHOOK_URL` |

---

## Po credential leaku — postup

1. **Okamžitě revokovat** starý klíč — nečekat na nic jiného
2. **Vyčistit Git historii:**
```bash
rm -rf .git
git init
git add .
git commit -m "fix: remove exposed credentials"
git remote add origin git@github.com:USER/REPO.git
git push --force origin master
```
3. **Vytvořit nový klíč** a aktualizovat v n8n credentials
4. **Zkontrolovat ostatní services** exponované ve stejném repu

---

## Pravidla

- GitHub secret scanning detekuje až po push — secrets jsou již veřejné. Nelze na to spoléhat.
- Boti skenují GitHub kontinuálně — "nikdo to nenajde" není ochrana.
- Živé credentials nikdy při testování na public repu.
- `.env` soubory nikdy do Gitu — pouze `.env.example` s placeholdery.
