# KoloPay — DevOps Case Study
*Private/NDA'd codebase — details generalized where appropriate. Happy to go deeper in an interview.*

## Context
KoloPay is a live fintech product (savings/e-commerce). I owned the containerization and deployment of `kolo-auth-service`, a Spring Boot (Java 21) microservice living inside a multi-module Maven monorepo with no root aggregator POM.

## Containerization
- Dockerized `kolo-auth-service` inside a multi-module Maven monorepo with no root aggregator POM — a non-trivial build-context problem, since Docker needs a coherent build context and Maven needs correct module resolution order.
- Wrote a multi-stage Dockerfile: the build stage compiles the shared libraries (`kolo-core`, `kolo-security`, `kolo-logging-core`, `kolo-openapi-core`) and the service's own module chain (`kolo-auth-entity`, `kolo-auth-datalayer`, `kolo-auth-service`) in correct dependency order; the runtime stage ships only the final JAR on a minimal, non-root JRE image.
- Diagnosed and fixed a real dependency-resolution build failure caused by missing shared-library modules in the Docker build context — the build was reaching for modules that weren't copied into the context, a classic monorepo-in-a-container problem.

## Local Development Environment
- Built `docker-compose.yml` running `auth-service` + PostgreSQL locally, with correct container networking and environment variable wiring (DB connection, JWT config).
- Established a `.env` / `.env.example` convention to separate real secrets from committed config templates, with proper `.gitignore` coverage — so nobody accidentally commits live credentials.

## Cloud Deployment (Hetzner)
- Manually provisioned a Hetzner Cloud VM (Ubuntu 24.04): configured a non-root deploy user, SSH key-based auth, `ufw` firewall rules, and `fail2ban` for brute-force protection.
- Evaluated a reverse-proxy (Caddy) setup for automatic TLS, then simplified to direct port exposure per a team decision — TLS wasn't viable yet since there was no registered domain.
- Debugged and resolved a live production issue: a mismatch between the cloud provider's firewall configuration and the OS-level firewall rules. The OS-level (`ufw`) config was correct, but traffic was still being blocked at the cloud infrastructure layer — a good reminder that "firewall configured" isn't one setting, it's a stack.
- Deployed and verified `auth-service` live and healthy over the public IP, confirmed via the `/actuator/health` endpoint and direct endpoint testing.

## CI/CD
- Built a GitHub Actions workflow (`deploy-auth.yml`) that auto-deploys `auth-service` to the Hetzner server on pushes to the `dev` branch, scoped via path filters so it only triggers on relevant module/config changes — avoiding unnecessary redeploys from unrelated commits.
- Currently debugging an SSH connection timeout between the GitHub-hosted runner and the server; isolated the issue to a firewall-level rule rather than the application itself.

## What this demonstrates
- Real-world Docker multi-stage builds in a non-trivial monorepo (not a toy single-repo app)
- End-to-end ownership: local dev → cloud provisioning → CI/CD → production verification
- Debugging skill across layers (application, OS, cloud infrastructure) rather than just "it worked on my machine"
- Process awareness — catching workflow and naming issues before they become team-wide problems
