# Cloud

> Provider-neutral cloud concepts. See specific provider folders for AWS/Azure/GCP.

---

## Purpose

Understand cloud concepts that apply across providers.

## Prerequisites

- [Linux/](../Linux/), [Docker/](../Docker/).

## Learning Outcome

You can reason about cloud architecture and pick providers.

## Dependencies

- A cloud account.

## Related Files

- [AWS/](../AWS/) · [Azure/](../Azure/) · [GCP/](../GCP/) · [Vercel/](../Vercel/) · [Netlify/](../Netlify/) · [Cloudflare/](../Cloudflare/) · [Deployment/](../Deployment/) · [System-Design/](../System-Design/)

## AI Instructions

When picking cloud:
1. **Default to managed services** (less ops).
2. **Default to smallest sufficient region**.
3. **Pin everything** (versions, regions, instance types).
4. **Set billing alerts** before anything else.
5. **Use IaC** (Terraform / Pulumi).
6. **Don't put secrets in env vars of CI** — use a vault.

## Human Notes

### Service categories
- **Compute** — VMs, containers, functions.
- **Storage** — object, block, file.
- **Database** — relational, document, cache, vector.
- **Networking** — VPC, load balancers, CDN, DNS.
- **Security** — IAM, KMS, WAF.
- **Monitoring** — logs, metrics, traces.
- **AI/ML** — model APIs, training, inference.

### Cross-provider concepts
| Concept | AWS | Azure | GCP |
|---|---|---|---|
| Compute (VM) | EC2 | VM | Compute Engine |
| Containers | ECS, Fargate | Container Apps, ACI | Cloud Run, GKE |
| Functions | Lambda | Functions | Cloud Functions |
| Object storage | S3 | Blob Storage | Cloud Storage |
| Relational DB | RDS, Aurora | SQL Database | Cloud SQL, Spanner |
| Cache | ElastiCache | Cache for Redis | Memorystore |
| CDN | CloudFront | Front Door | Cloud CDN |
| DNS | Route 53 | DNS | Cloud DNS |
| VPC | VPC | VNet | VPC |
| IAM | IAM | Entra ID | IAM |
| KMS | KMS | Key Vault | KMS |
| Secrets | Secrets Manager | Key Vault | Secret Manager |
| Queue | SQS | Service Bus | Pub/Sub |
| Stream | Kinesis | Event Hubs | Dataflow |
| Search | OpenSearch | Cognitive Search | Vertex AI Search |
| Vector DB | (use pgvector / RDS) | (use AI Search) | Vertex AI Vector Search |
| Functions | Lambda | Functions | Cloud Functions |

### Pricing model
- Pay-as-you-go.
- Reserved instances (1-3 yr commitment, big discount).
- Spot/preemptible (cheap, can be killed).
- Free tiers (use them, watch the limits).

### Multi-cloud
- Avoid if possible. Operational cost is huge.
- Use multi-cloud only for: compliance, latency, vendor lock-in avoidance.

### Vendor lock-in
- Real but often overstated.
- Weigh: speed of building vs cost of switching.
- Prefer open standards (Postgres, Docker, Kubernetes).

### IaC (Infrastructure as Code)
- **Terraform** (industry default).
- **Pulumi** (real languages).
- **OpenTofu** (open-source Terraform fork).
- **AWS CDK** (TypeScript/Python).
- **Azure Bicep**.
- **Cloud Deployment Manager** (GCP).

### Cost optimization
- Right-size instances.
- Use Spot for batch.
- Reserved for steady workloads.
- Delete unused resources.
- Use S3 lifecycle policies.
- Set billing alerts.
- Use cost explorer.

### Security
- IAM roles > access keys.
- Least privilege.
- MFA on root.
- Secrets in vault.
- Encryption at rest + in transit.
- VPC + private subnets.
- Security groups (allowlist).
- WAF for web apps.
- CloudTrail / Audit Logs / Cloud Audit Logs for auditing.

### Reliability
- Multi-AZ (availability zone).
- Multi-region for global HA.
- Backups (and test restores!).
- Health checks.
- Auto-scaling.
- Disaster recovery plan.

## Common Mistakes

- ❌ No billing alerts (surprise bills).
- ❌ Over-provisioned resources.
- ❌ Resources in wrong region.
- ❌ Secrets in env vars.
- ❌ No backups.
- ❌ Single AZ.
- ❌ Manual infrastructure (no IaC).
- ❌ Open security groups (0.0.0.0/0).

## Tools

- Terraform: https://www.terraform.io/
- Pulumi: https://www.pulumi.com/
- OpenTofu: https://opentofu.org/
- AWS CLI, gcloud, az.

## References

- AWS Well-Architected: https://aws.amazon.com/architecture/well-architected/
- Azure Architecture Center: https://learn.microsoft.com/azure/architecture/
- Google Cloud Architecture Framework: https://cloud.google.com/architecture/framework

## Further Reading

- *Cloud Native Patterns* — Jonathan Johnson
- *Designing Data-Intensive Applications* — Martin Kleppmann

## Exercises

1. Deploy a 3-tier app to AWS / GCP / Azure.
2. Set up IaC with Terraform.
3. Add cost alerts + budget.

## Projects

- Build a multi-region app with failover.

---

**Previous:** [Linux/](../Linux/) · **Next:** [Vercel/](../Vercel/) · **Related:** [Deployment/](../Deployment/)
