# Group Project: Secure System Architecture Deployment

This repository contains the configuration and source code for deploying a securely integrated system architecture using Docker Compose. The environment consists of a PostgreSQL database backend, an administrative dashboard (PgAdmin4), and a headless Content Management System (Strapi) application.

## Project Contributors

1. Pichayut Sombun / 6702041510113 / s6702041510113@email.kmutnb.ac.th
2. Chawanwit Manthanom / 6702041510024 / ezmt011146@gmail.com
3. Apichart Thijaroen / 6702041510211 / s6702041510211@email.kmutnb.ac.th
4. Thanicha Suanwong / 6702041510059 / s6702041510059@email.kmutnb.ac.th

## System Components

- **Database**: PostgreSQL 15 (Alpine)
- **Management Application**: PgAdmin4
- **Application Server**: Strapi CMS

## Security Principles Implemented

The primary objective of this architecture is to ensure a secure environment. The following measures have been applied:

1. **Isolated Internal Network**: The database is enclosed within a non-accessible Docker internal network. It can only be accessed by associated containers running within the same virtual network space (`internal_network`).
2. **Restricted Port Exposure**: Direct external access to the PostgreSQL database (default port 5432) is denied. The port is not bound to the host machine. Management must be done securely via the PgAdmin4 dashboard or by the internal backend application.
3. **Environment Isolation for Credentials**: Secrets and passwords are not hardcoded. The configuration strictly relies on an external `.env` variables file for storing sensitive credentials.
4. **Controlled Initialization Process**: System components depend on the health and state of the database (`depends_on`). This eliminates race conditions where backend software cannot connect properly during startup.

## Deployment Instructions

### Prerequisites

- Docker Engine and Docker Compose must be installed on the host machine.

### Setup and Execution

1. Clone the project repository to your local machine.
2. Initialize environment variables: Duplicate the provided `.env.example` file and rename it to `.env`.
3. Configure the variables inside the `.env` file with secure and unique passwords.
4. Execute the deployment command from within the project directory:

```bash
docker compose up -d
```

### Accessing the Services

Once the containers have successfully initialized, you can access the respective services via a web browser:

- **PgAdmin4 Dashboard**: `http://localhost:5050`
- **Strapi Application**: `http://localhost:1337`

To safely shut down and halt all running services, use the following command:

```bash
docker compose down
```
