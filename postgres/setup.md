# PostgreSQL Database

## Starting postgresql container

```bash

docker run -itd -e POSTGRES_USER=falconcodes -e POSTGRES_PASSWORD=2147483647 -p 5432:5432 -v postgres_data:/var/lib/postgresql/data --name postgres_db postgres

```

## Starting postgresql shell

```bash

docker exec -it postgres_db psql -U falconcodes db_name

```
