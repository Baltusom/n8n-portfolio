# Phase 4 / Module 2 — Error Handling & Robustness

## What was done
- Error Trigger added to Lead-Intake-Pipeline (main workflow)
- Ai-agent already had an Error Trigger from Phase 3
- WF7-rag-search: Qdrant URL fixed to `http://qdrant:6333`
- Ai-agent: lead webhook URL fixed to `http://n8n:5678`

## Pattern
Every main workflow has a standalone Error Trigger → Discord notification.
Sub-workflows handle their own validation via IF nodes.
