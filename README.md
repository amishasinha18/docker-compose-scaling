# Microservices Horizontal Scaling with Docker Compose

A hands-on DevOps project demonstrating how to horizontally scale backend microservices on demand using Docker Compose to handle sudden high traffic scenarios (e.g., peak exam traffic or high concurrent user load).

---

## 📌 Architecture Overview

Instead of scaling an entire monolithic application or vertically adding hardware limits, microservices allow scaling only the bottleneck service independently.

```text
Users / Inbound Requests
           ↓
Docker Dynamic Port Routing
     ┌─────┼─────┐
     ↓     ↓     ↓
 backend backend backend
 (Replica 1) (Replica 2) (Replica 3)

 ⚙️ Tech Stack & Key Concepts
Containerization & Orchestration: Docker, Docker Compose

Runtime & Framework: Node.js, Express.js

Key Concepts Covered:

Microservices Architecture

Horizontal Scaling vs. Vertical Scaling

Port Conflict Resolution (Dynamic Ephemeral Ports vs. Fixed Bindings)

Stateful vs. Stateless Workloads

🚀 How to Run & Scale
1. Build and Spin Up Replicas
Scale the backend service directly to 3 instances:

Bash
docker compose up --build --scale backend=3
2. Verify Active Containers & Mapped Ports
In a separate terminal tab, inspect the running containers:

Bash
docker compose ps
Docker will assign dynamic host ports to each container (e.g., 62655, 62656, 62658) to avoid host port collision (3000:3000).

3. Test Container Responses
Send requests to each active port to observe individual container hostname identities:

Bash
curl http://localhost:<ASSIGNED_PORT>
Sample Output:

Plaintext
Response from backend container: bb5cfaf6c3d2
📉 Scaling Down (Resource Optimization)
Once peak demand normalizes, avoid overprovisioning by scaling instances back down without downtime:

Bash
docker compose up -d --scale backend=1
🛑 Teardown
Stop and remove all running containers and networks:

Bash
docker compose down