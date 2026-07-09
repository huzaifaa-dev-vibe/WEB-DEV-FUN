# GCP

> Google Cloud. Strong in data, AI, and containers (K8s was born here).

---

## Purpose

Use GCP for apps, especially data-heavy or AI workloads.

## Prerequisites

- [Cloud/](../Cloud/), [Linux/](../Linux/).

## Learning Outcome

You can deploy and operate GCP-backed apps.

## Dependencies

- GCP account.

## Related Files

- [AWS/](../AWS/) · [Azure/](../Azure/) · [Cloud/](../Cloud/) · [Kubernetes/](../Kubernetes/)

## AI Instructions

When using GCP:
1. Set billing alerts.
2. Use managed services (Cloud Run, Cloud SQL, etc.).
3. Use Cloud Run for containers (serverless).
4. Use GKE for Kubernetes.
5. Use BigQuery for analytics.
6. Use Vertex AI for ML.
7. IaC with Terraform.

## Human Notes

### Core services
- **Compute Engine** — VMs.
- **Cloud Run** — serverless containers (best in class).
- **GKE** — managed Kubernetes.
- **Cloud Functions** — serverless functions.
- **App Engine** — PaaS (older).
- **Cloud Storage** — object storage.
- **Cloud SQL** — managed Postgres/MySQL/SQL Server.
- **Spanner** — distributed SQL (PlanetScale-like).
- **Firestore** — document DB.
- **Bigtable** — wide-column.
- **Memorystore** — managed Redis.
- **BigQuery** — analytics warehouse.
- **Pub/Sub** — messaging.
- **Cloud Tasks** — task queue.
- **Cloud Build** — CI/CD.
- **Cloud CDN** — CDN.
- **Cloud Load Balancing** — LB.
- **Cloud DNS** — DNS.
- **Secret Manager** — secrets.
- **Vertex AI** — ML platform.
- **Gemini API** — Google's LLMs.

### CLI
```bash
gcloud auth login
gcloud config set project my-project
gcloud run deploy --source .
gcloud sql instances create ...
```

### Cloud Run (best in class)
- Serverless containers.
- Scale to zero.
- Pay per request.
- Multi-region.

```dockerfile
# Dockerfile
FROM node:20-alpine
# ...
```
```bash
gcloud run deploy myapp --source . --region us-central1 --allow-unauthenticated
```

### BigQuery
- Petabyte-scale analytics.
- SQL.
- Pay per query (or flat rate).
- Best-in-class for analytics.

### When to use GCP
- Data / analytics workloads (BigQuery).
- AI / ML (Vertex AI, Gemini).
- Containers (Cloud Run, GKE).
- Multi-region serverless.

### When NOT to use
- Need AWS ecosystem.
- Enterprise Microsoft stack.

## Common Mistakes

- ❌ No billing alerts.
- ❌ Wrong region.
- ❌ Open firewall rules.
- ❌ Secrets in code.

## Tools

- GCP docs: https://cloud.google.com/docs
- gcloud CLI: https://cloud.google.com/sdk/gcloud
- Firebase (mobile + web): https://firebase.google.com/

## References

- Google Cloud Architecture Framework: https://cloud.google.com/architecture/framework

## Exercises

1. Deploy a container to Cloud Run.
2. Set up Cloud SQL + Secret Manager.
3. Build a BigQuery analytics dashboard.

## Projects

- Build a serverless app on Cloud Run + Cloud SQL + BigQuery.

---

**Previous:** [Azure/](../Azure/) · **Next:** [Monitoring/](../Monitoring/) · **Related:** [Cloud/](../Cloud/)
