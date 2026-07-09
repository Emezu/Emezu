<h1 align="center">Hi, I'm Blessing Fabian 👋</h1>
<h3 align="center">Junior DevOps / Cloud Engineer | Docker · Kubernetes · Terraform · AWS · CI/CD</h3>

<p align="center">
  <a href="https://www.linkedin.com/in/blessingfabian/"><img src="https://img.shields.io/badge/LinkedIn-0077B5?style=flat&logo=linkedin&logoColor=white"></a>
</p>

---

### 🎯 What I do
I build and automate cloud infrastructure, I write CI/CD pipelines, contenarize microservices and manage applications to ensure scalability and availability. I'm currently looking for a **Junior DevOps / Cloud Engineer** role where I can own real infrastructure and keep growing.

### 🧰 Core Stack
| Category | Tools |
|---|---|
| **Cloud** | AWS (EC2, S3, VPC, IAM, Auto Scaling, ECS, SQS) | Hetzner | GCP | Microsoft Azure
| **IaC** | Terraform |
| **Containers** | Docker, Docker compose | Kubernetes |
| **CI/CD** | GitHub Actions, Jenkins |
| **Scripting/OS** | Bash, YAML, Linux (Ubuntu) |
| **Version Control** | Git |


### 💼 Professional Case Study — KoloPay (Fintech, Private Repo)
End-to-end DevOps ownership of a Spring Boot microservice's containerization and deployment for a live fintech product, in a multi-module Java monorepo.

**Containerization**
- Dockerized `kolo-auth-service` (Java 21 / Spring Boot) inside a multi-module Maven monorepo with no root aggregator POM, a non-trivial build-context problem.
- Wrote a multi-stage Dockerfile: build stage compiles shared libraries and the service's module chain in correct dependency order; runtime stage ships only the final JAR on a minimal, non-root JRE image.
- Diagnosed and fixed a real dependency-resolution failure caused by missing shared-library modules in the Docker build context.

**Local Dev Environment**
- Built `docker-compose.yml` running the service + PostgreSQL with correct networking and env-var wiring (DB, JWT config).
- Established a `.env` / `.env.example` convention with proper `.gitignore` coverage to keep secrets out of version control.

**Cloud Deployment (Hetzner)**
- Manually provisioned and hardened a Hetzner Cloud VM (Ubuntu 24.04): non-root deploy user, SSH key auth, `ufw` firewall, `fail2ban`.
- Evaluated a reverse-proxy (Caddy) setup, then simplified to direct port exposure per team decision (no registered domain yet, so TLS wasn't viable).
- Debugged and resolved a live deployment blocker caused by a mismatch between the cloud provider's firewall rules and the OS-level firewall rules — despite correct `ufw` config, external traffic was still blocked at the cloud layer.
- Deployed and verified the service healthy in production via its health-check endpoint and live endpoint testing.

**CI/CD**
- Built a GitHub Actions workflow that auto-deploys the service to the Hetzner server on pushes to `dev`, scoped with path filters so it only triggers on relevant module/config changes.
- Currently debugging an SSH timeout between the GitHub-hosted runner and the server, isolated to a firewall-level rule rather than the app.

**Process & Collaboration**
- Flagged a branch-strategy gap (`infra` vs `main` vs `dev`) and helped clarify the intended promotion flow.
- Documented the full build-and-deploy process so the same containerization pattern can be repeated across four upcoming services in the same monorepo.

### 📌 Featured Projects
- **[Docker-SERVICE](https://github.com/Emezu/Docker-SERVICE)** — Containerized a Node.js app and shipped it to AWS EC2 via a GitHub Actions CI/CD pipeline.
- **[IAC-BEST-PRACTICE-PROJECT](https://github.com/Emezu/IAC-BEST-PRACTICE-PROJECT)** — Provisioned a VPC, EC2 fleet, and Auto Scaling Group using Terraform, following IaC best practices (modules, remote state, variables).
- **Secure Kubernetes CI/CD Pipeline** — Multi-stage pipeline for deploying K8s workloads with automated provisioning and secrets management.
- **[Kubenet_class](https://github.com/Emezu/Kubenet_class)** — Hands-on repo practicing Kubernetes deployment strategies (rolling updates, blue/green).
- **Linux Server Monitoring Script** — Bash tooling that reports on server performance/health.
- **Log Archiving Automation Tool** — Scheduled Bash script for compressing, archiving, and rotating logs.

### 📈 GitHub Stats
<p align="center">
  <img src="https://github-readme-stats.vercel.app/api?username=Emezu&show_icons=true&theme=default&count_private=true" height="165">
  <img src="https://github-readme-stats.vercel.app/api/top-langs/?username=Emezu&layout=compact" height="165">
</p>

### 🌱 Currently Learning / Exploring
- Monitoring & observability (Prometheus, Grafana)
- Advanced Kubernetes (Helm, service mesh)
- AWS certification (Solutions Architect / SysOps Associate)

### 🤝 Let's Connect
Open to junior DevOps/Cloud roles and collaboration. Reach me via [LinkedIn](https://www.linkedin.com/in/blessingfabian) or [email](mailto:emezufabian@gmail.com).
