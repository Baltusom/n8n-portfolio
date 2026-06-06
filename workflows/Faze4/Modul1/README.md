# Fáze 4 / Modul 1 — Produkční infrastruktura

## Stack
- n8n + PostgreSQL 16 + Qdrant 1.18.1 + Uptime Kuma v jednom Docker Compose
- Společná Docker network `n8n-net`
- Persistent volumes pro všechna data
- Autostart při rebootu přes systemd (`n8n-prod.service`)
- ngrok free plan se statickou doménou jako tunnel
- Uptime Kuma monitoring — 3 monitory (n8n, Qdrant, webhook)

## Soubory
- `~/n8n-prod/docker-compose.yml`
- `~/n8n-prod/.env`
- `/etc/systemd/system/n8n-prod.service`
