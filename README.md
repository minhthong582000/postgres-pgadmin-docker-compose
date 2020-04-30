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

Create 2 file in postgres-pgadmin-docker-compose directory named pgadmin.env and postgres.env, add the following:

> pgadmin.env

```
PGADMIN_DEFAULT_EMAIL=youremail@something.com
PGADMIN_DEFAULT_PASSWORD=pgadmin
PGADMIN_LISTEN_PORT=5050
```

> postgres.env

```
POSTGRES_PASSWORD=postgres
```

You can change the value of email and password variables to whatever you want.

Go to: [pgadmin-container-deployment](https://www.pgadmin.org/docs/pgadmin4/development/container_deployment.html#environment-variables) and [postgres-docker-hub](https://hub.docker.com/_/postgres?tab=description) to fill in any configurations that are important for you.

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
Username: postgres
Password: your password from postgres.env, default: pgadmin
```

## Connect to PostgresSQL server

Open terminal on your local machine, run:

```
psql -H localhost -p 5432 -U <your username>
```

## Authors

-   **Minh Thong** - _Initial work_ - [minhthong582000](https://github.com/minhthong582000)

> Feel free for contributing, pull requests and issues are always welcome!
