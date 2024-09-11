# Postgres Docker Compose Setup

This repository contains a Docker Compose configuration to set up a PostgreSQL database container using the `postgres:latest` image. It provides an easy way to spin up a PostgreSQL instance for local development or testing purposes.

## Getting Started

### Prerequisites

Before you begin, ensure you have the following installed on your system:

- [Docker](https://docs.docker.com/get-docker/)
- [Docker Compose](https://docs.docker.com/compose/install/)

### Installation and Setup

1. **Clone the repository** to your local machine:
   ```bash
   git clone https://github.com/black-spidera/postgres-docker.git
   cd postgres-docker
   ```

2. **Build and start the PostgreSQL service for the first time** by running:
   ```bash
   docker compose -f docker-compose.yml up --build
   ```

   - For subsequent runs, you can start the service with:
     ```bash
     docker compose -f docker-compose.yml up
     ```

   - This will:
     - Download the `postgres:latest` Docker image (if not already available).
     - Start a container named `postgres-container`.
     - Expose PostgreSQL on port `5432` for local access.
     - Persist database data in a Docker volume named `postgres-data`.

3. **Access the PostgreSQL container**:
   - To access the PostgreSQL shell in the running container:
     ```bash
     docker exec -it postgres-container psql -U postgres
     ```
   - This command opens the PostgreSQL prompt where you can manage your database.

4. **Stop and remove containers**:
   To stop and remove the running containers and networks:
   ```bash
   docker compose down
   ```

   If you also want to remove the persistent volume (which will delete all database data), add the `-v` flag:
   ```bash
   docker compose down -v
   ```

### Configuration

- **Database name**: `medusajs`
- **Username**: `postgres`
- **Password**: `postgres`
- **Port**: `5432`

You can modify these configurations in the `docker-compose.yml` file under the `environment` section.

### Accessing the Database

You can connect to the running PostgreSQL container using a PostgreSQL client like `psql`, PgAdmin, DBeaver, or any other tool that supports PostgreSQL.

Example connection string:
```
postgresql://postgres:postgres@localhost:5432/medusajs
```

Alternatively, to directly access the database shell inside the container, run:
```bash
docker exec -it postgres-container psql -U postgres
```

### Persistent Data

The database data is stored in a Docker volume named `postgres-data`. This ensures that the database persists across container restarts, and you won't lose your data unless the volume is explicitly removed.

### Troubleshooting

- **Port Binding Error**: If you get an error like `bind: address already in use`, it means another service is already using port `5432`. You can either stop that service or modify the `docker-compose.yml` to use a different port.

