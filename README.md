# Learn-DB

**English** · [Русский](README.ru.md)

A small educational PostgreSQL project using Docker Compose and Adminer. Includes a sample online-store table for SQL practice.

## Requirements

- [Docker Desktop](https://www.docker.com/products/docker-desktop/) (or Docker Engine with the Compose plugin)
- An available local port **8080** for Adminer and **5432** for PostgreSQL (change `POSTGRES_PORT` in `.env` if needed)

## Quick start

```bash
git clone https://github.com/mirasayon/Learn-DB.git
cd Learn-DB
docker compose up -d
```

Open **http://localhost:8080** and sign in to Adminer:

| Field | Value |
| --- | --- |
| System | PostgreSQL |
| Server | `postgres` |
| Username | `student` |
| Password | `learn_db_demo_only` |
| Database | `expdb` |

These are **demo credentials** from the tracked `.env` file. The database `expdb` is created on the first startup.

**Connection addresses:** inside Compose, use `postgres:5432`. From your computer (for example, with a database client), use `localhost:5432`. PostgreSQL and Adminer are bound to `127.0.0.1`, not publicly exposed.

## Practice: online-store products

In Adminer, open **SQL command**, copy the contents of [`sql/products.sql`](sql/products.sql) into the editor, and execute them **in the `expdb` database**.

The script creates a `products` table with an automatically generated ID, a nonnegative price and stock count, creation/update timestamps, and a trigger that updates `updated_at` when a product changes. It does **not** delete existing data or insert example products.

Try these queries in **SQL command**, one at a time:

```sql
INSERT INTO products (name, description, price, stock, category)
VALUES ('USB-C cable', '1 meter', 9.90, 20, 'Accessories');

SELECT * FROM products;

UPDATE products SET price = 8.50 WHERE name = 'USB-C cable';

SELECT name, price, updated_at FROM products;
```

## Docker commands

| Task | Command |
| --- | --- |
| Start PostgreSQL and Adminer | `docker compose up -d` |
| Start only PostgreSQL | `docker compose up -d postgres` |
| Check status | `docker compose ps` |
| PostgreSQL logs | `docker compose logs -f postgres` |
| Stop containers | `docker compose stop` |
| Start stopped containers | `docker compose start` |
| Restart PostgreSQL | `docker compose restart postgres` |
| Remove containers/network, keep data | `docker compose down` |
| **Delete all local database data** | `docker compose down -v` |

## Troubleshooting

- **`postgres` cannot be resolved:** use `postgres` (not `localhost`) in Adminer's **Server** field, and start both services with `docker compose up -d`.
- **Port already in use:** change `POSTGRES_PORT` in `.env` if port 5432 is busy. Port 8080 is configured in `compose.yaml`.
- **Login fails after editing `.env`:** PostgreSQL uses `POSTGRES_USER` / `POSTGRES_PASSWORD` / `POSTGRES_DB` only when initializing an **empty** database volume. Existing roles and passwords are not automatically changed. For a disposable learning database, run `docker compose down -v` and then `docker compose up -d` to reinitialize it; **this permanently deletes all database data**.
- **No tables in Adminer:** the SQL example is not loaded automatically. Run [`sql/products.sql`](sql/products.sql) as described above.

> **Learning environment only:** `.env` is intentionally committed with disposable example credentials for convenience. Never use these credentials on a public server or for a real service. Replacing credentials in Git's latest commit does not remove them from previous commits.
