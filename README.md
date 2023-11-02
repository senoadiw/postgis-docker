# postgis-docker
Run PostgresSQL 15 with PostGIS 3.3.x on Docker.

Based on the following images:
* https://registry.hub.docker.com/r/postgis/postgis/
* https://registry.hub.docker.com/_/adminer

## Requirements
* Docker and Docker Compose installed
  * https://docs.docker.com/engine/install/
* for Linux: the user must belong the docker group to allow running `docker` without `sudo` privilege
  * `sudo usermod -aG docker ${USER}`

## How to run
SSH to the target server and run:
```
git clone https://github.com/senoadiw/postgis-docker.git

cd postgis-docker

cp .env.sample .env

# optional: edit the default db details
nano .env

# bring up the containers
docker compose up -d

# check the logs and wait a moment for the containers to initialize
docker compose logs -f

docker compose logs postgres -f

# done!

# run psql on the default postgres database
docker compose exec -it postgres psql -U pguser postgres

# to list the databases
docker compose exec -it postgres psql -U pguser -l

# to stop the containers
docker compose stop

# to start the containers
docker compose up -d

# to delete the containers
docker compose down

# to delete the containers and volumes (warning: this will delete ALL databases)
docker compose down -v
```

## Connecting to the database
Using tools such as pgAdmin or DBeaver, it is possible to connect to the database from the Docker host. Refer to the database credentials in the `.env` file and set the host to `localhost` and port to `6432` (which is mapped to port `5432` in the `postgres` container).

Adminer is also available by accessing `http://localhost:8080` and entering the following connection details:
* System: PostgreSQL
* Server: postgres
* Username: refer to the `.env` file
* Password: refer to the `.env` file
* Database: refer to the `.env` file
