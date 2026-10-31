# Learn-DB

[English](README.md)

Простой учебный проект: PostgreSQL + Docker + Adminer.

## Запуск

```sh
docker compose up -d
```

Открой http://localhost:8080 и войди в Adminer:

| Поле | Значение |
| --- | --- |
| System | PostgreSQL |
| Server | `postgres` |
| Username | `student` |
| Password | `learn_db_demo_only` |
| Database | `expdb` |

Таблица `products` создаётся **автоматически при первом запуске**.

## Примеры SQL

В Adminer открой **SQL command** и выполни запросы по очереди:

```sql
INSERT INTO products (name, price, stock, category)
VALUES ('Mouse', 15.90, 10, 'Electronics');

SELECT * FROM products;

UPDATE products SET price = 12.50 WHERE name = 'Mouse';

DELETE FROM products WHERE name = 'Mouse';
```

Структура таблицы находится в [sql/products.sql](sql/products.sql).

## Остановка и сброс

- `docker compose down` — остановить и удалить контейнеры, сохранив данные БД.
- `docker compose down -v` — **безвозвратно удалить все локальные данные БД**.

Если проект уже запускался раньше, SQL-скрипт **не выполнится повторно** для существующего тома. Чтобы создать таблицу без удаления данных, запусти [sql/products.sql](sql/products.sql) вручную в Adminer.

Тестовые данные для входа и порт PostgreSQL указаны в [`.env`](.env). Изменение логина или пароля там не меняет уже созданную БД. PostgreSQL и Adminer доступны только с этого компьютера. **Не используй тестовый пароль в настоящих сервисах.**
