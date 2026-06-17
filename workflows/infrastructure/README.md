# Phase 4 / Module 1 — Production Infrastructure

## Stack
- n8n + PostgreSQL 16 + Qdrant 1.18.1 + Uptime Kuma in a single Docker Compose
- Shared Docker network `n8n-net`
- Persistent volumes for all data
- Autostart on reboot via systemd (`n8n-prod.service`)
- ngrok free plan with a static domain as the tunnel
- Uptime Kuma monitoring — 3 monitors (n8n, Qdrant, webhook)

## Files
- `~/n8n-prod/docker-compose.yml`
- `~/n8n-prod/.env`
- `/etc/systemd/system/n8n-prod.service`
