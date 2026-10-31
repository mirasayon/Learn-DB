# Learn-DB

A minimal PostgreSQL practice database with Docker Compose.

## Start

Install Docker, then run:

```sh
docker compose up -d --remove-orphans
```

On a new database volume, PostgreSQL automatically creates the `products` table from [sql/products.sql](sql/products.sql).

## Connect with DBeaver

Open **DBeaver** → **New Database Connection** → **PostgreSQL** and enter:

| Setting | Value |
| --- | --- |
| Host | `localhost` |
| Port | `5432` |
| Database | `expdb` |
| Username | `student` |
| Password | `learn_db_demo_only` |

Click **Test Connection** (install the PostgreSQL driver if prompted), then **Finish**.

Open an **SQL Editor** for `expdb` and try:

```sql
SELECT * FROM products;

INSERT INTO products (name, price, stock)
VALUES ('Mouse', 15.90, 10);

SELECT * FROM products;
```

## Stop

```sh
docker compose down
```

This keeps database data. **`docker compose down -v` deletes all local database data.**

If you have an existing database volume, the initialization script does not run again; execute [sql/products.sql](sql/products.sql) once in DBeaver if `products` is missing. Connection settings can be changed in [`.env`](.env), but changing credentials there does not update an existing database. The credentials are for local learning only.
