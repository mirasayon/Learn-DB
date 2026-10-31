# Learn-DB

An empty PostgreSQL database with Docker Compose.

## Start

```sh
docker compose up -d
```

## DBeaver

Create a new **PostgreSQL** connection using:

| Setting | Value |
| --- | --- |
| Host | `localhost` |
| Port | `5432` |
| Database | `test` |
| Username | `postgres` |
| Password | `1234` |

Click **Test Connection**, then **Finish**. Edit the settings in [`.env`](.env) if needed.

## Stop

```sh
docker compose down
```

Data stays in the Docker volume. **`docker compose down -v` permanently deletes the database data.**

Local learning use only; do not use the example password in production.
