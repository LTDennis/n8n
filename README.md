# Minimal AI Stack

This is a clean Docker setup that includes:

- ✅ n8n (Automation)
- ✅ Ollama (LLM like LLaMA3, Qwen, Mistral, etc.)
- ✅ PostgreSQL (Database for n8n)
- ✅ Caddy (HTTPS reverse proxy with Let's Encrypt)

## Setup

1. Clone this repo and `cd` into it.
2. Replace `yourdomain.com` in `Caddyfile` with your real domain.
3. Point your domain to your server IP (A record).
4. Run:

```bash
docker compose up -d
```

## Update

```bash
docker compose pull
```

## (Optional) Remove old/unused images

```bash
docker image prune -f
```

## Ports

- n8n: https://yourdomain.com/n8n/
- Ollama: https://yourdomain.com/ollama/

Caddy will automatically provision HTTPS.

----------------------------------------------------


🛠️ Upgrade Steps: PostgreSQL 15 → 16 (or latest)

## Step 1: Backup your DB

```bash
docker exec -t postgres pg_dumpall -U n8n > backup.sql
```

Or to back up just the n8n database:

```bash
docker exec -t postgres pg_dump -U n8n n8n > n8n_backup.sql
```

## Step 2: Stop and remove the current container

```bash
docker compose down
```
**The volume is not deleted, just the container.

##Step 3: Change image version in <b>docker-compose.yml</b>
```bash
# Before
image: postgres:15

# After (example)
image: postgres:16
```

##Step 4: Start fresh container

```bash
docker compose up -d
```

##Step 5: Restore your database if needed

```bash
docker exec -i postgres psql -U n8n < backup.sql
```

⚠️ Tip: Stay within the same major version if possible

If you're on postgres:15, use postgres:15.6 to stay safe unless you need new features.

## 🔁 Optional: Automate minor patch upgrades only

```bash
image: postgres:15  # Pulls latest patch of v15 (e.g., 15.6)
```

Then you can safely run:

```bash
docker compose pull postgres
docker compose up -d
```
