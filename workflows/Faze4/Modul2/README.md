# Fáze 4 / Modul 2 — Error handling & robustnost

## Co bylo uděláno
- Error Trigger přidán do Lead-Intake-Pipeline (hlavní workflow)
- Ai-agent měl Error Trigger již z Fáze 3
- WF7-rag-search: Qdrant URL opravena na `http://qdrant:6333`
- Ai-agent: lead webhook URL opravena na `http://n8n:5678`

## Pattern
Každý hlavní workflow má standalone Error Trigger → Discord notifikace.
Sub-workflows řeší vlastní validaci přes IF nody.
