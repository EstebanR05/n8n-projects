# Postgres + pgAdmin (Docker Compose)

Este proyecto levanta:

- `postgres-server` (PostgreSQL)
- `pgadmin-server` (UI para administrar PostgreSQL)
- `n8n-server` (n8n)

## Puertos

- PostgreSQL: `localhost:15432`
- pgAdmin: `http://localhost:18082`
- n8n: `http://localhost:15678`

## Credenciales de PostgreSQL

- User: `postgres`
- Password: `12345`
- Database: `local`

URI de conexión:

`postgresql://postgres:12345@localhost:15432/local`

## Credenciales de pgAdmin

- Email: `admin@admin.com`
- Password: `admin`

## Uso

```bash
docker compose up -d
docker compose ps
```

## Configuracion de n8n

n8n usa la misma base de datos de este compose mediante estas variables:

- `DB_TYPE=postgresdb`
- `DB_POSTGRESDB_HOST=postgres-server`
- `DB_POSTGRESDB_PORT=5432`
- `DB_POSTGRESDB_DATABASE=local`
- `DB_POSTGRESDB_USER=postgres`
- `DB_POSTGRESDB_PASSWORD=12345`

## Nota

Los datos de PostgreSQL se guardan en el volumen `postgres-server-data` y la data de n8n en `./n8n_data`.
