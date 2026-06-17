# Phase 4 / Module 3 — Showcase Project: AI Lead Qualification & Support Bot

## Description
Full AI pipeline for the OptimiumAI agency. Receives leads and questions 24/7, qualifies them, answers from a knowledge base, and stores them in Notion CRM.

## Workflows
The showcase project uses the final workflows from Phase 3:
- `workflows/lead-intake-pipeline/` — Lead Intake Pipeline (4 sub-workflows)
- `workflows/ai-agent-rag/` — AI Agent + RAG pipeline (WF5, WF6b, WF7)

> Note: the RAG knowledge base source is excluded from this public repo to protect client data. The ingestion workflow (`WF6b-rag-ingestion-markdown`) shows how any markdown source is chunked, embedded, and loaded into Qdrant.
