# Learning Journey

This folder is the build history behind the production workflows in [`../workflows/`](../workflows/).
It is kept for reference — to show how the showcase evolved — and is **not** the deployable version.
For the current, production-ready workflows, use the top-level `workflows/` directory.

| Folder | Stage | What it shows |
|--------|-------|---------------|
| `phase2-pipeline-v1/` | First lead pipeline | Single linear workflow: webhook → enrichment → Notion + Discord |
| `phase3-m1-subworkflow-architecture/` | Refactor to sub-workflows | Same pipeline split into enrich / classify / notify via Execute Workflow nodes |
| `phase3-m2-ollama-agent/` | First AI agent | Early agent built on local Ollama (later replaced by the Claude + RAG version) |
| `notes/` | Build notes | Error-handling approach, showcase description, and portfolio notes |

The final versions of each of these now live in `workflows/lead-intake-pipeline/` and `workflows/ai-agent-rag/`.
