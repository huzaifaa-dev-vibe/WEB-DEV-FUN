# AWS

> Amazon Web Services. The biggest cloud. Use managed services.

---

## Purpose

Use AWS for production apps: EC2, S3, Lambda, RDS, ECS, and more.

## Prerequisites

- [Cloud/](../Cloud/), [Linux/](../Linux/).

## Learning Outcome

You can deploy, scale, and operate an AWS-backed app.

## Dependencies

- AWS account.

## Related Files

- [Cloud/](../Cloud/) · [Azure/](../Azure/) · [GCP/](../GCP/) · [Deployment/](../Deployment/) · [Docker/](../Docker/) · [Kubernetes/](../Kubernetes/)

## AI Instructions

When using AWS:
1. **Set billing alerts first.**
2. **Use IAM roles, not access keys** when possible.
3. **Use managed services** (RDS, ElastiCache, SQS).
4. **Multi-AZ** for HA.
5. **Use IaC** (Terraform / CDK).
6. **Pin regions** (latency + compliance).
7. **Don't use `root` account** for daily work.

## Human Notes

### Core services
- **EC2** — VMs.
- **S3** — object storage.
- **RDS** — managed relational DBs (Postgres, MySQL, etc.).
- **Aurora** — AWS's high-perf RDS.
- **Lambda** — serverless functions.
- **ECS / Fargate** — container orchestration.
- **EKS** — managed Kubernetes.
- **CloudFront** — CDN.
- **Route 53** — DNS.
- **IAM** — identity.
- **KMS** — key management.
- **Secrets Manager** — secrets.
- **VPC** — virtual network.
- **CloudWatch** — logs / metrics.
- **SQS** — queue.
- **SNS** — pub/sub.
- **Kinesis** — streams.
- **DynamoDB** — NoSQL.
- **ElastiCache** — Redis/Memcached.
- **OpenSearch** — search.
- **Bedrock** — managed LLMs.
- **SageMaker** — ML platform.
- **Cognito** — user pools / auth.

### Free tier
- EC2 t2.micro: 750 hours/month for 12 months.
- S3: 5GB + 20k GETs / 2k PUTs.
- Lambda: 1M requests + 400k GB-sec/month.
- RDS: 750 hours/month for 12 months.
- CloudFront: 50GB out + 2M requests/month.

### Common patterns

#### Static site + CDN
- S3 bucket + CloudFront + Route 53.

#### Container app
- ECS Fargate + ALB + RDS.

#### Serverless API
- Lambda + API Gateway + DynamoDB.

#### Next.js on AWS
- OpenNext (SST) — deploy Next.js to AWS.

### Pricing
- Pay-as-you-go.
- Reserved Instances (1-3 yr): up to 75% off.
- Spot Instances: up to 90% off (interruptible).
- Savings Plans: commit to $/hour.

### IaC
- **AWS CDK** (TypeScript / Python) — best DX.
- **Terraform** — multi-cloud.
- **CloudFormation** — AWS-native (verbose).
- **SAM** — serverless.

### CLI
```bash
aws configure
aws s3 ls
aws ec2 describe-instances
aws lambda invoke --function-name myfunc out.json
aws logs tail /aws/lambda/myfunc
```

### Tips
- Use **AWS CDK** for IaC.
- Use **SST** for Next.js on AWS.
- Use **DynamoDB** only if you understand single-table design (otherwise Postgres).
- Use **RDS Proxy** for connection pooling.
- Use **Aurora Serverless v2** for variable workloads.
- Use **CloudFront** in front of everything.
- Use **WAF** for web apps.

## Common Mistakes

- ❌ No billing alerts (surprise bills!).
- ❌ Resources in wrong region.
- ❌ Open security groups (0.0.0.0/0).
- ❌ Access keys in code.
- ❌ Single-AZ for prod.
- ❌ Manual infrastructure (no IaC).
- ❌ EFS for things that should be S3.
- ❌ DynamoDB without understanding RCUs/WCUs.

## Tools

- AWS docs: https://docs.aws.amazon.com/
- AWS CLI: https://aws.amazon.com/cli/
- AWS CDK: https://aws.amazon.com/cdk/
- SST (Next.js on AWS): https://sst.dev/
- LocalStack (local AWS): https://localstack.cloud/
- aws-vault: https://github.com/99designs/aws-vault

## References

- AWS docs: https://docs.aws.amazon.com/
- AWS Well-Architected: https://aws.amazon.com/architecture/well-architected/
- Last Week in AWS: https://www.lastweekinaws.com/

## Further Reading

- *AWS Certified Solutions Architect Study Guide* — for the basics
- *The AWS Workbook* — Jon Bonso

## Exercises

1. Deploy a static site to S3 + CloudFront.
2. Run a container app on ECS Fargate.
3. Build a serverless API with Lambda + DynamoDB.

## Projects

- Build a multi-AZ, multi-region app on AWS.

---

**Previous:** [Cloudflare/](../Cloudflare/) · **Next:** [Azure/](../Azure/) · **Related:** [Cloud/](../Cloud/)
