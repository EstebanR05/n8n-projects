# n8n Local Docker Setup

This project runs `n8n` with `PostgreSQL` using Docker Compose.

## Services

- `n8n` (UI): `http://localhost:5678`
- `postgres` (internal to compose): host `postgres`, port `5432`

## Current Auth Model

This stack uses **two login layers**:

1. Basic Auth (from `docker-compose.yml`)
2. n8n internal user management (owner account stored in DB)

### Basic Auth Credentials

- Email/User: `admin@example.com`
- Password: `admin123`

## Start / Stop

```bash
cd ~/projects/n8n-projects/n8n-local-docker
sudo docker compose up -d
sudo docker compose ps
```

Stop:

```bash
sudo docker compose down
```

## First Login Flow

1. Open `http://localhost:5678`
2. Pass Basic Auth with:
   - `admin@example.com`
   - `admin123`
3. In n8n setup/login, use a valid email format (example: `you@example.com`)

## Common Errors and Fixes

### `Must be a valid email`

Cause: n8n requires email format in the login/signup form.

Fix: use an actual email format, for example `admin@example.com`.

### `Wrong username or password. Do you have caps lock on?`

Cause: n8n internal owner credentials are wrong (different from Basic Auth), or owner state is inconsistent.

Fix (reset n8n user management):

```bash
cd ~/projects/n8n-projects/n8n-local-docker
sudo docker compose exec n8n n8n user-management:reset
sudo docker compose restart n8n
```

Then open `http://localhost:5678` and create the owner again.

### `ERR_CONNECTION_REFUSED` / site not reachable

Check containers:

```bash
sudo docker compose ps
sudo docker compose logs --tail=120 n8n
sudo docker compose logs --tail=120 postgres
```

If Docker daemon permission fails:

```bash
sudo usermod -aG docker $USER
newgrp docker
docker ps
```

## Database Config Used by n8n

From `docker-compose.yml`:

- `DB_TYPE=postgresdb`
- `DB_POSTGRESDB_HOST=postgres`
- `DB_POSTGRESDB_PORT=5432`
- `DB_POSTGRESDB_DATABASE=n8n`
- `DB_POSTGRESDB_USER=n8n`
- `DB_POSTGRESDB_PASSWORD=n8n`

## Data Persistence

- Postgres data volume: `postgres_data`
- n8n data volume: `n8n_data`

To remove everything (including DB and users):

```bash
sudo docker compose down -v --remove-orphans
```
