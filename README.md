# Postgres-pgadmin-docker-compose

A recipe to setup PostgreSQL and pgAdmin4 easily and quickly with Docker and Docker-compose.

## Getting Started

### Prerequisites

-   Docker CE
-   Docker-compose

### Installing

Clone this repo to your local machine using:

```
git clone https://github.com/minhthong582000/postgres-pgadmin-docker-compose.git
cd postgres-pgadmin-docker-compose
```

Before install, you need to pass environment variables from an external file to docker-compose.yaml within the ‘env_file’ option.

Create 2 files in postgres-pgadmin-docker-compose directory named pgadmin.env and postgres.env, add the following:

> pgadmin.env

```
PGADMIN_DEFAULT_EMAIL=youremail@something.com
PGADMIN_DEFAULT_PASSWORD=pgadmin
PGADMIN_LISTEN_PORT=5050
```

> postgres.env

```
POSTGRES_USER=pguser
POSTGRES_PASSWORD=pgpassword
POSTGRES_DB=pgdatabase
```

You can change the value to whatever you want.

For more information, go to [pgadmin-container-deployment](https://www.pgadmin.org/docs/pgadmin4/development/container_deployment.html#environment-variables) or [postgres-docker-hub](https://hub.docker.com/_/postgres?tab=description), and fill in any configurations that are important for you.

To install it simply do following from your terminal:

```
docker-compose up -d
```

## Configure pgAdmin 4

Go to your web browser and navigate to:

```
http://localhost:5050/
```

You will see pgadmin login panel

Enter your email and password from pgadmin.env file

Add a server with:

```
Hostname: postgres
Port: 5432
Maintenance database: your database from postgres.env, default: pgdatabase
Username: your username from postgres.env, default: pguser
Password: your password from postgres.env, default: pgpassword
```

### pgAdmin: Connect to Postgres database running on your local machine

There are many way to access database running on docker host from a container. See [stack-overflow](https://stackoverflow.com/questions/24319662/from-inside-of-a-docker-container-how-do-i-connect-to-the-localhost-of-the-mach).

-   On Docker for mac and Docker for windows:

> Use hostname: host.docker.internal

-   On Docker for Linux:

Run pgAdmin with the host mode by changing docker-compose configuration to:

> docker-compose.yaml

```
version: "3.7"
services:
    pgadmin:
        image: dpage/pgadmin4
        container_name: pgadmin
        restart: always
        env_file:
            - ./pgadmin.env
        ports:
            - "5050:5050"
        volumes:
            - pga4volume:/var/lib/pgadmin
        network_mode: host
```

Then

> Use hostname: localhost

## Connect to PostgresSQL server

Open terminal on your local machine, run:

```
psql -h localhost -p 5432 -U <your username>
```

## Authors

-   **Minh Thong** - _Initial work_ - [minhthong582000](https://github.com/minhthong582000)

> Feel free for contributing, pull requests and issues are always welcome!
