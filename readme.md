## Docker

Start PostgreSQL only:

```bash
docker compose up -d postgres
```

Start PostgreSQL and Adminer:

```bash
docker compose up -d
```

Adminer: <http://localhost:8080>

Show container status:

```bash
docker compose ps
```

Show PostgreSQL logs:

```bash
docker compose logs -f postgres
```

Restart PostgreSQL:

```bash
docker compose restart postgres
```

Stop containers without removing them:

```bash
docker compose stop
```

Start previously stopped containers:

```bash
docker compose start
```

Stop and remove containers and the Compose network:

```bash
docker compose down
```

Delete containers, network and PostgreSQL volume:

```bash
docker compose down -v
```
