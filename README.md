# n8n Automation Portfolio — OptimiumAI

> Production-ready n8n workflows for AI automation, lead qualification, and RAG pipelines.  
> Built by [Frank](https://linkedin.com/in/yourprofile) @ [OptimiumAI](https://optimiumai.com)

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
  Faze1/          # Basic workflows (RSS, Webhook, Cron)
  Faze2/          # Intermediate (Lead Intake Pipeline v1)
  Faze3/
    Modul1/       # Sub-workflow architecture (Lead Intake Pipeline v2)
    Modul2/       # AI Agent with Ollama
    Modul3/       # AI Agent + RAG pipeline (production version)
  Faze4/
    Modul1/       # Production infrastructure (Docker Compose)
    Modul2/       # Error handling & robustness
knowledge/
  optimiumAI-knowledge-base.md   # RAG knowledge base source
```

---

## 🔧 Workflows

### Phase 1 — Basics
| Workflow | Description |
|----------|-------------|
| rss-ai-discord | RSS feed → AI filter → Discord notification |
| webhook-google-sheets | Webhook → data processing → Google Sheets |
| cron-coingecko-gmail | Cron → CoinGecko API → Gmail report |

### Phase 2 — Intermediate
| Workflow | Description |
|----------|-------------|
| Lead-Intake-Pipeline | Webhook → enrichment → Notion CRM + Discord |

### Phase 3 — Advanced (Production)
| Workflow | Description |
|----------|-------------|
| Lead-Intake-Pipeline | Main orchestrator with sub-workflows |
| Lead-Intake-Pipeline-enrich | Hunter.io email enrichment |
| Lead-Intake-Pipeline-classify | Lead scoring |
| Lead-Intake-Pipeline-notify | Notion CRM + Discord notification |
| Ai-agent | Claude Haiku agent with RAG + tools |
| WF6b-rag-ingestion-markdown | Knowledge base ingestion into Qdrant |
| WF7-rag-search | Vector search sub-workflow |

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

See `Faze4/Modul1/README.md` for deployment guide.

---

## 🚀 Quick Start

### Prerequisites
- Docker & Docker Compose
- Anthropic API key
- Ollama with `nomic-embed-text` model

### Deploy

```bash
git clone https://github.com/Baltusom/n8n-portfolio.git
cd n8n-portfolio/workflows/Faze4/Modul1

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
| Workflow Automation | from €500/project |
| AI Agent Development | from €1,500/project |
| RAG Pipeline | from €2,000/project |
| Consultation | €150/hour |

**Book a free 30-min discovery call:** [calendly.com/optimiumai/discovery](https://calendly.com/optimiumai/discovery)

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
