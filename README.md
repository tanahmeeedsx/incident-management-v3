# Incident Management — Dockerized Application

A full-stack Incident Management application containerized using Docker and Docker Compose. The project demonstrates multi-container application deployment with React, Node.js, Express, PostgreSQL, persistent storage, and container health checks.

## Overview

This project builds on the previous manual and automated EC2 deployment versions by introducing Docker-based containerization.

The frontend, backend, and PostgreSQL database run as separate containers, managed through Docker Compose. Nginx serves the React application and forwards API requests to the backend service.

## Features

- Dockerized React frontend
- Containerized Node.js and Express backend
- PostgreSQL database container
- Multi-container orchestration with Docker Compose
- Persistent PostgreSQL storage using Docker volumes
- Container health checks
- Environment-based configuration
- Docker multi-stage frontend build
- Dedicated Dockerfiles and `.dockerignore` files

## Technology Stack

| Layer | Technology |
|---|---|
| Frontend | React, Vite |
| Backend | Node.js, Express.js |
| Database | PostgreSQL 16 |
| Web Server | Nginx |
| Containerization | Docker |
| Orchestration | Docker Compose |
| Base Images | Node.js Alpine, Nginx Alpine |
| Development Environment | Linux |

## Architecture

The application uses a multi-container architecture managed by Docker Compose.

```text
                 User
                  |
                  v
          Frontend Container
             Nginx :80
                  |
             API Requests
                  |
                  v
          Backend Container
           Express :5000
                  |
                  v
          Database Container
          PostgreSQL :5432
                  |
                  v
          Persistent Volume
```

## Project Structure

```text
incident-management-v3/
├── backend/
│   ├── src/
│   ├── Dockerfile
│   └── .dockerignore
├── frontend/
│   ├── src/
│   ├── Dockerfile
│   ├── nginx.conf
│   └── .dockerignore
├── compose.yaml
├── .env
├── .gitignore
└── README.md
```

## Run Locally with Docker

### Prerequisites

- Docker Engine
- Docker Compose

### 1. Clone the Repository

```bash
git clone https://github.com/tanahmeeedsx/incident-management-v3.git
cd incident-management-v3
```

### 2. Configure Environment Variables

Create a `.env` file in the project root:

```env
DB_NAME=incidentdb
DB_USER=incident_user
DB_PASSWORD=your_strong_password
```

Keep `.env` out of Git.

### 3. Build the Docker Images

```bash
docker compose build
```

### 4. Start the Application

```bash
docker compose up -d
```

### 5. Verify Container Status

```bash
docker compose ps
```

All three services should become healthy.

## Application Access

| Service | URL |
|---|---|
| Frontend | http://localhost:8080 |
| Backend Health Check | http://localhost:8080/health |
| Incidents API | http://localhost:8080/api/incidents |

## Useful Docker Commands

View running containers:

```bash
docker compose ps
```

View application logs:

```bash
docker compose logs -f
```

View individual service logs:

```bash
docker compose logs -f backend
```

Stop the application:

```bash
docker compose down
```

Stop containers without deleting database data:

```bash
docker compose down
```

Stop containers and remove persistent database data:

```bash
docker compose down -v
```

## Containerization Highlights

- Separate containers for frontend, backend, and database services.
- Docker Compose manages service dependencies and startup order.
- PostgreSQL data persists through a named Docker volume.
- Health checks verify database, backend, and frontend availability.
- Multi-stage frontend builds separate build dependencies from the production Nginx image.
- `.dockerignore` files reduce unnecessary build context.
- Internal Docker networking enables service-to-service communication.

## What I Learned

- Building custom Docker images for full-stack applications.
- Understanding Dockerfiles and multi-stage builds.
- Orchestrating multiple services with Docker Compose.
- Configuring container networking and service discovery.
- Managing persistent database storage with Docker volumes.
- Implementing container health checks.
- Handling environment variables and container logs.
- Optimizing Docker build contexts.

## Project Evolution

This project is the third stage of the Incident Management DevOps learning series.

| Version | Focus |
|---|---|
| V1 | AWS EC2 Manual Deployment |
| V2 | Automated Deployment with Bash and Nginx |
| V3 | Docker Containerization |
| V4 | Monitoring and Observability |

## Author

**Tanjim Ahmed (Tomal)**

DevOps Engineer | Linux | Docker | CI/CD | AWS | Kubernetes

GitHub: [@tanahmeeedsx](https://github.com/tanahmeeedsx)

LinkedIn: [Tanjim Ahmed](https://linkedin.com/in/tanahmedd/)

Built as a hands-on project to strengthen practical knowledge of Docker, container orchestration, and modern DevOps deployment workflows.
