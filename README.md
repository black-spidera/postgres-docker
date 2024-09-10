# Postgres Docker Compose Setup

This repository contains a Docker Compose configuration to set up a PostgreSQL database container using `postgres:latest` image. It provides an easy way to spin up a PostgreSQL instance for local development or testing purposes.

## Getting Started

### Prerequisites

Before you begin, ensure you have the following installed on your system:

- [Docker](https://docs.docker.com/get-docker/)
- [Docker Compose](https://docs.docker.com/compose/install/)

### Installation and Setup

1. Clone the repository to your local machine:
   ```bash
   git https://github.com/black-spidera/postgres-docker.git
   cd postgres-docker
   ```

2. To start the PostgreSQL service, run:
   ```bash
   docker-compose up -d
   ```

   This command will:
   - Download the `postgres:latest` Docker image if it is not already available.
   - Start a new container named `postgres-container`.
   - Expose PostgreSQL on port `5432` for local access.
   - Persist the database data in a Docker volume named `postgres-data`.

3. To stop and remove the containers and networks, run:
   ```bash
   docker-compose down
   ```

   If you also want to remove the persistent volume (which will delete the database data), add the `-v` flag:
   ```bash
   docker-compose down -v
   ```

### Configuration

- **Database name**: `medusajs`
- **Username**: `postgres`
- **Password**: `postgres`
- **Port**: `5432`

You can modify the database name, username, and password in the `docker-compose.yml` file under the `environment` section if needed.

### Accessing the Database

You can access the running PostgreSQL container using any PostgreSQL client (e.g., `psql`, PgAdmin, DBeaver, etc.).

Example connection string:
```
postgresql://postgres:postgres@localhost:5432/medusajs
```

Alternatively, you can run the following command to enter the container's shell:
```bash
docker exec -it postgres-container psql -U postgres
```

### Volumes

The database data is stored in a named volume `postgres-data` to ensure persistence across container restarts.

## License

This project is licensed under the MIT License. See the [LICENSE](LICENSE) file for details.
