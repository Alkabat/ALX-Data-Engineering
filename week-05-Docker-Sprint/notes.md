Notes
1. Introduction to Docker & Containerization
•	Docker provides OS-level virtualization via containers, packaging code, runtime, system tools, libraries, and settings into a single portable unit.
•	Unlike traditional VMs, containers share the host kernel, making them lighter, faster to start, and more resource-efficient.
•	Core Docker objects: images (read-only templates), containers (running instances), networks, and volumes.
•	Docker architecture: Docker Client → Docker Daemon → Registries (e.g., Docker Hub).
2. Working with Containers & Images
•	Images act as blueprints; containers are instantiated from them.
•	Key commands practiced: docker run, docker ps, docker stop/start, docker rm, docker images, docker rmi.
•	Dockerfile basics: FROM, RUN, COPY, WORKDIR, EXPOSE, CMD/ENTRYPOINT.
•	Built custom images, pushed to Docker Hub, and managed repositories.
3. Docker Networking
•	Default networks: bridge, host, none; created custom networks for service isolation and communication.
•	Containers on the same user-defined network can resolve each other by service/container name (DNS).
•	Practiced commands: docker network create/inspect/rm, attaching containers to networks, and basic network troubleshooting.
4. Volumes & Data Persistence
•	Containers are ephemeral; volumes ensure data persists beyond container lifecycle.
•	Used named volumes (db-data) for PostgreSQL data, and understood differences between volumes, bind mounts, and tmpfs.
•	Applied best practices: avoid storing persistent data in container layers; use volumes for databases and stateful services.
5. Docker Compose
•	Docker Compose orchestrates multi-container apps via a single docker-compose.yml.
•	Defined services (api, db, web), custom network (app-network), and named volume (db-data).
•	Key commands: docker compose up/down/ps/logs, scaling services, updating images, and forcing recreates.
•	Implemented health checks and performed rollback from nginx:1.25 → nginx:1.24 using --force-recreate.
6. Best Practices, Resource Management & Troubleshooting
•	Distinguished between image optimization (layer caching, minimal base images) and runtime resource constraints (CPU/memory limits).
•	Learned to check service logs first when troubleshooting performance issues after scaling.
•	Considered orchestration options (Docker Swarm vs Kubernetes) for future scaling and HA needs.
