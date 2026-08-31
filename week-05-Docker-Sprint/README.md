# Docker Sprint – Weekly Update

## Overview
This week I completed the Docker sprint in my data engineering journey, focusing on containerization fundamentals, multi-service orchestration with Docker Compose, and practical troubleshooting.

## Topics Covered
- Introduction to Docker & containerization
- Docker images, Dockerfiles, and custom image management
- Docker networking (bridge, custom networks, service discovery)
- Volumes and data persistence
- Docker Compose for multi-service applications
- Best practices: image optimization, resource constraints, security, and orchestration overview

## Practical Exercises

### 1. Docker Compose Multi-Service Application
- Built a stack with three services: `api` (Node.js), `db` (PostgreSQL), and `web` (Nginx).
- Connected the API to PostgreSQL using the service name `db` over a custom network `app-network`.
- Used a named volume `db-data` to persist PostgreSQL data.
- Nginx acted as a reverse proxy to the API.
- Practiced `docker compose up`, `ps`, and configuration troubleshooting.

### 2. Docker Compose Service Update, Health Check & Rollback
- Upgraded Nginx from `nginx:alpine` to `nginx:1.25`.
- Added a `curl`-based health check; troubleshot a failing `wget` health check.
- Confirmed `nginx:1.25` as healthy via `docker compose ps` and `docker inspect`.
- Rolled back to `nginx:1.24` using `docker compose up --force-recreate`.
- Verified rollback through `ps`, `logs`, and `docker inspect`.

### 3. Docker Troubleshooting & Resource Management
- Differentiated image optimization strategies from container resource constraints.
- Considered CPU/memory limits and application load when tuning performance.
- Applied the principle: “check service logs first” when diagnosing performance issues after scaling.

## Key Commands Used
- `docker compose up/down/ps/logs`
- `docker compose up --force-recreate`
- `docker network create/inspect`
- `docker volume create/inspect`
- `docker build/push/pull`

## Outcomes
- Confidently containerized a Node.js API with PostgreSQL.
- Orchestrated multi-service apps with networking and persistent storage.
- Implemented health checks and performed safe rollbacks.
- Strengthened troubleshooting skills around logs, networks, and resource constraints.
