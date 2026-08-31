Reflection
This Docker sprint moved me from “running single containers” to “orchestrating real application stacks.” The biggest shift was thinking in terms of services, networks, and volumes instead of isolated containers.
The multi-service exercise made the concepts concrete: using service names (db) for connectivity, isolating traffic with app-network, and ensuring data survival with db-data showed how Docker Compose mirrors real-world microservice deployments.
The health check and rollback exercise was particularly valuable. Moving from nginx:alpine to a specific version (1.25), then deliberately rolling back to 1.24, taught me how to validate changes and recover safely—critical skills for production environments.
Finally, distinguishing image optimization from runtime resource constraints clarified where to focus when performance issues arise. Going forward, I’ll prioritize checking logs first, then consider scaling and resource limits, before diving into deeper network or application debugging.
Next, I plan to:
•	Experiment with multi-stage builds to further optimize images.
•	Explore basic Docker Swarm or a local Kubernetes setup to understand orchestration beyond Compose.
•	Integrate these patterns into a small end-to-end data pipeline project.

