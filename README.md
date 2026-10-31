# Learn-DB

[Русский](README.ru.md)

A small PostgreSQL playground with Docker and Adminer.

## Start

```sh
docker compose up -d
```

Open http://localhost:8080 and log in:

| Field | Value |
| --- | --- |
| System | PostgreSQL |
| Server | `postgres` |
| Username | `student` |
| Password | `learn_db_demo_only` |
| Database | `expdb` |

The `products` table is created automatically **on the first start**.

## Try SQL

In Adminer, open **SQL command** and run these statements one at a time:

```sql
INSERT INTO products (name, price, stock, category)
VALUES ('Mouse', 15.90, 10, 'Electronics');

SELECT * FROM products;

UPDATE products SET price = 12.50 WHERE name = 'Mouse';

DELETE FROM products WHERE name = 'Mouse';
```

The table definition is in [sql/products.sql](sql/products.sql).

## Stop or reset

- `docker compose down` — stop and remove containers; keep database data.
- `docker compose down -v` — **permanently delete all local database data**.

If you already started this project before, the initialization script will **not** run again on an existing database volume. To create the table without deleting your data, run [sql/products.sql](sql/products.sql) manually in Adminer.

The demo login and PostgreSQL host port are in [`.env`](.env). Changing database credentials there does not change an already initialized database. PostgreSQL and Adminer are accessible only from this computer. **Do not use the demo password for real services.**
