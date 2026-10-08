# Learn-DB

[English](README.md) · **Русский**

Небольшой учебный проект с PostgreSQL, Docker Compose и Adminer. Есть пример таблицы интернет-магазина для практики SQL.

## Что понадобится

- [Docker Desktop](https://www.docker.com/products/docker-desktop/) (либо Docker Engine с плагином Compose)
- Свободные локальные порты **8080** для Adminer и **5432** для PostgreSQL (порт PostgreSQL можно изменить в `.env`)

## Быстрый запуск

```bash
git clone https://github.com/mirasayon/Learn-DB.git
cd Learn-DB
docker compose up -d
```

Открой **http://localhost:8080** и войди в Adminer:

| Поле | Значение |
| --- | --- |
| System | PostgreSQL |
| Server | `postgres` |
| Username | `student` |
| Password | `learn_db_demo_only` |
| Database | `expdb` |

Это **тестовые данные** из файла `.env`, который намеренно хранится в Git. При первом запуске автоматически создаётся база `expdb`.

**Адрес подключения:** между контейнерами используй `postgres:5432`. Для подключения с компьютера через клиент БД — `localhost:5432`. PostgreSQL и Adminer доступны только локально (через `127.0.0.1`).

## Практика: товары интернет-магазина

В Adminer открой **SQL command**, скопируй содержимое файла [`sql/products.sql`](sql/products.sql) в редактор и выполни запрос **в базе `expdb`**.

Скрипт создаёт таблицу `products` с автоматическим ID, проверкой неотрицательной цены и остатка, временем создания/изменения и триггером для обновления `updated_at`. Существующие данные он не удаляет и товары не добавляет.

Попробуй выполнить эти запросы в **SQL command** по очереди:

```sql
INSERT INTO products (name, description, price, stock, category)
VALUES ('USB-C cable', '1 meter', 9.90, 20, 'Accessories');

SELECT * FROM products;

UPDATE products SET price = 8.50 WHERE name = 'USB-C cable';

SELECT name, price, updated_at FROM products;
```

## Команды Docker

| Действие | Команда |
| --- | --- |
| Запустить PostgreSQL и Adminer | `docker compose up -d` |
| Запустить только PostgreSQL | `docker compose up -d postgres` |
| Посмотреть состояние | `docker compose ps` |
| Логи PostgreSQL | `docker compose logs -f postgres` |
| Остановить контейнеры | `docker compose stop` |
| Запустить остановленные | `docker compose start` |
| Перезапустить PostgreSQL | `docker compose restart postgres` |
| Удалить контейнеры и сеть, сохранив данные | `docker compose down` |
| **Удалить все данные локальной БД** | `docker compose down -v` |

## Частые проблемы

- **Не найден сервер `postgres`:** в поле **Server** укажи `postgres`, а не `localhost`, и запусти оба контейнера: `docker compose up -d`.
- **Порт занят:** если занят 5432, измени `POSTGRES_PORT` в `.env`. Порт 8080 указан в `compose.yaml`.
- **Ошибка входа после изменения `.env`:** `POSTGRES_USER`, `POSTGRES_PASSWORD` и `POSTGRES_DB` используются при первой инициализации **пустого** тома PostgreSQL. В существующей БД они не меняются автоматически. Если данные не нужны, выполни `docker compose down -v`, затем `docker compose up -d`; **все данные БД будут безвозвратно удалены**.
- **В Adminer нет таблиц:** SQL-файл не запускается автоматически. Выполни [`sql/products.sql`](sql/products.sql) вручную.

> **Только для учёбы:** `.env` специально хранится в Git с нейтральными демонстрационными данными. Не используй эти пароли для реальных сервисов или на публичном сервере. Замена пароля в текущем коммите не удаляет его из предыдущих коммитов Git.
