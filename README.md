# n8n Automation Portfolio — OptimiumAI

> Production-ready n8n workflows for AI automation, lead qualification, and RAG pipelines.  
> Built by Ondrej M. @ OptimiumAI

---

## 🚀 Showcase: AI Lead Qualification & Support Bot

Full AI pipeline that qualifies leads and answers questions 24/7 using RAG knowledge base.

**Live demo:** [Chat with the agent](https://gulf-evidence-blob.ngrok-free.dev/webhook/8ab77f1d-28dd-448d-b409-baf7a7e64f3e/chat)

**Stack:** n8n · Claude Haiku 4.5 · Qdrant · PostgreSQL · Docker · Ollama

```
Chat / Webhook → AI Agent (Claude) → RAG Search (Qdrant)
                                   → Lead Submit → Notion CRM + Discord
```

---

## 📁 Repository Structure

```
workflows/
  basics/                 # 3 standalone demos (RSS → AI → Discord, Webhook → Sheets, Cron → Gmail)
  lead-intake-pipeline/   # Lead qualification: webhook → enrich → score → Notion CRM + Discord
  ai-agent-rag/           # Claude agent + RAG retrieval over Qdrant
  infrastructure/         # Production Docker Compose stack + deployment guide
learning/                 # Build journey — earlier iterations of the above, kept for reference
docs/                     # Security guidelines
portfolio/                # Architecture screenshots
```

> The RAG knowledge base source is intentionally excluded from this public repo to protect client data.
> `learning/` documents how the showcase evolved; the production-ready versions live under `workflows/`.

---

## 🔧 Workflows

### `basics/`
| Workflow | Description |
|----------|-------------|
| rss-ai-discord | RSS feed → AI filter → Discord notification |
| webhook-google-sheets | Webhook → data processing → Google Sheets |
| cron-coingecko-gmail | Cron → CoinGecko API → Gmail report |

### `lead-intake-pipeline/` — sub-workflow architecture
| Workflow | Description |
|----------|-------------|
| Lead-Intake-Pipeline | Main orchestrator (Execute Workflow nodes) |
| Lead-Intake-Pipeline-enrich | Hunter.io email enrichment |
| Lead-Intake-Pipeline-classify | Lead scoring |
| Lead-Intake-Pipeline-notify | Notion CRM + Discord notification |

### `ai-agent-rag/`
| Workflow | Description |
|----------|-------------|
| Ai-agent | Claude Haiku agent with RAG + tools |
| WF6b-rag-ingestion-markdown | Knowledge base ingestion into Qdrant |
| WF7-rag-search | Vector search sub-workflow (Ollama embed → Qdrant REST) |

---

## 🏗️ Infrastructure

Production stack runs on Docker Compose:

```yaml
Services:
  - n8n          (workflow engine)
  - PostgreSQL   (n8n database)
  - Qdrant       (vector database)
  - Uptime Kuma  (monitoring)
```

See `workflows/infrastructure/README.md` for deployment guide.

---

## 🚀 Quick Start

### Prerequisites
- Docker & Docker Compose
- Anthropic API key
- Ollama with `nomic-embed-text` model

### Deploy

```bash
git clone https://github.com/Baltusom/n8n-portfolio.git
cd n8n-portfolio/workflows/infrastructure

# Configure environment
cp .env.example .env
nano .env  # Add your credentials

# Start stack
docker compose up -d
```

### Import Workflows
1. Open n8n UI at `http://localhost:5678`
2. Import JSON files in this order:
   - Sub-workflows first (enrich, classify, notify)
   - Main workflows after
   - AI agent last

---

## 💼 Services

Built with this stack for clients:

| Service | Price |
|---------|-------|
| Workflow Automation | from €250/project |
| AI Agent Development | from €700/project |
| RAG Pipeline | from €1200/project |
| Consultation | €45/hour |

**Book a free 30-min discovery call:** https://calendly.com/ondrej-motovsky

---

## 🛠️ Tech Stack

- **Workflow engine:** n8n (self-hosted)
- **AI:** Claude Haiku 4.5 (Anthropic), Ollama (local)
- **Vector DB:** Qdrant
- **Database:** PostgreSQL, Notion
- **Integrations:** Hunter.io, Discord, Google Workspace
- **Infrastructure:** Docker, Ubuntu, Cloudflare

---

## 📄 License

MIT — feel free to use as reference for your own automation projects.

---

*OptimiumAI — Automate smarter, grow faster.*
