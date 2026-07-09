# Docker

> Containerize anything. Ship anywhere.

---

## Purpose

Master Docker: Dockerfile, compose, multi-stage, buildkit, best practices.

## Prerequisites

- Linux basics, [Backend/](../Backend/).

## Learning Outcome

You can containerize an app, write docker-compose, optimize images.

## Dependencies

- Docker installed.

## Related Files

- [Kubernetes/](../Kubernetes/) · [Deployment/](../Deployment/) · [CI-CD/](../CI-CD/) · [Linux/](../Linux/)

## AI Instructions

When using Docker:
1. **Multi-stage builds** — small final image.
2. **Pin base image** (`node:20.11-alpine`, not `node:latest`).
3. **Non-root user** in container.
4. **`.dockerignore`** to skip node_modules, .git, etc.
5. **Layer caching** — copy package.json before source.
6. **Healthcheck** in Dockerfile.
7. **Read-only filesystem** where possible.
8. **Distroless / alpine** for smaller images.

## Human Notes

### Multi-stage Node Dockerfile
```dockerfile
# deps
FROM node:20-alpine AS deps
WORKDIR /app
COPY package*.json ./
RUN npm ci

# builder
FROM node:20-alpine AS builder
WORKDIR /app
COPY --from=deps /app/node_modules ./node_modules
COPY . .
RUN npm run build

# runner
FROM node:20-alpine AS runner
WORKDIR /app
ENV NODE_ENV=production
RUN addgroup -g 1001 nodejs && adduser -S nextjs -u 1001
COPY --from=builder --chown=nextjs:nodejs /app/.next/standalone ./
COPY --from=builder --chown=nextjs:nodejs /app/.next/static ./.next/static
COPY --from=builder --chown=nextjs:nodejs /app/public ./public
USER nextjs
EXPOSE 3000
ENV PORT=3000
HEALTHCHECK CMD wget --spider http://localhost:3000/health || exit 1
CMD ["node", "server.js"]
```

### .dockerignore
```
node_modules
.next
.git
*.md
.env*
Dockerfile
docker-compose.yml
```

### docker-compose.yml
```yaml
services:
  web:
    build: .
    ports:
      - "3000:3000"
    environment:
      - DATABASE_URL=postgres://user:pass@db:5432/app
    depends_on:
      db:
        condition: service_healthy

  db:
    image: postgres:16-alpine
    environment:
      POSTGRES_USER: user
      POSTGRES_PASSWORD: pass
      POSTGRES_DB: app
    volumes:
      - db-data:/var/lib/postgresql/data
    healthcheck:
      test: ["CMD-SHELL", "pg_isready -U user"]
      interval: 5s
      retries: 5

  redis:
    image: redis:7-alpine
    volumes:
      - redis-data:/data

volumes:
  db-data:
  redis-data:
```

### Commands
```bash
docker build -t myapp .
docker run -p 3000:3000 myapp
docker compose up -d
docker compose logs -f web
docker compose exec web sh
docker compose down
docker system prune -a
```

### Best practices
- Pin versions (no `latest`).
- Multi-stage.
- Small base (alpine, distroless).
- Non-root user.
- HEALTHCHECK.
- Read-only where possible.
- `.dockerignore`.
- Layer caching (rarely-changing first).
- BuildKit (`DOCKER_BUILDKIT=1`).
- `docker scan` for vulnerabilities.

### BuildKit
```bash
DOCKER_BUILDKIT=1 docker build .
```
Faster, parallel, cache from/to registry.

### Multi-platform builds
```bash
docker buildx build --platform linux/amd64,linux/arm64 -t myapp .
```

### Volumes vs bind mounts
- Volume: Docker-managed, persistent.
- Bind mount: host directory, for dev.

### Networking
- Default bridge.
- Custom networks for compose services.
- `host` mode (avoid in prod).

### Image scanning
- `docker scan` (Snyk).
- `trivy image myapp`.
- GitHub Container Registry scans.

### Registry
- Docker Hub (public, rate-limited).
- GitHub Container Registry (ghcr.io).
- AWS ECR, GCP AR, Azure ACR.
- Cloudflare Container Registry.

## Common Mistakes

- ❌ `latest` tag.
- ❌ Running as root.
- ❌ No multi-stage (huge images).
- ❌ No `.dockerignore` (slow builds, leaks).
- ❌ No healthcheck.
- ❌ Secrets in ENV of Dockerfile.
- ❌ No version pinning.

## Tools

- Docker docs: https://docs.docker.com/
- Compose spec: https://compose-spec.io/
- Dive (inspect layers): https://github.com/wagoodman/dive
- Trivy (scan): https://github.com/aquasecurity/trivy
- Hadolint (Dockerfile linter): https://github.com/hadolint/hadolint
- docker-slim: https://github.com/slimtoolkit/slim

## Further Reading

- *Docker Deep Dive* — Nigel Poulton

## Exercises

1. Containerize a Node app with multi-stage.
2. Set up compose with web + Postgres + Redis.
3. Scan your image with Trivy.

## Projects

- Build a production Docker setup with healthcheck, non-root, multi-platform.

---

**Previous:** [Deployment/](../Deployment/) · **Next:** [Kubernetes/](../Kubernetes/) · **Related:** [CI-CD/](../CI-CD/)
