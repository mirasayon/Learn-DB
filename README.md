# Learn-DB

A simple PostgreSQL database for SQL practice.

## Start

```sh
docker compose up -d
```

## Connect with DBeaver

Create a **PostgreSQL** connection:

| Setting | Value |
| --- | --- |
| Host | `localhost` |
| Port | `5432` |
| Database | `expdb` |
| Username | `student` |
| Password | `learn_db_demo_only` |

Click **Test Connection**, then **Finish**. The `products` table is created automatically on first startup.

## Try SQL

```sql
SELECT * FROM products;

INSERT INTO products (name, price, stock)
VALUES ('Mouse', 15.90, 10);
```

## Stop

```sh
docker compose down
```

Data is preserved. **`docker compose down -v` deletes all database data.**

For local learning only; do not use these credentials in production.
