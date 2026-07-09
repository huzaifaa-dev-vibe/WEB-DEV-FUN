# Azure

> Microsoft's cloud. Enterprise default, especially on Windows.

---

## Purpose

Use Azure for apps, especially enterprise / Windows / .NET workloads.

## Prerequisites

- [Cloud/](../Cloud/), [Linux/](../Linux/).

## Learning Outcome

You can deploy and operate Azure-backed apps.

## Dependencies

- Azure account.

## Related Files

- [AWS/](../AWS/) · [GCP/](../GCP/) · [Cloud/](../Cloud/) · [.NET/](../.NET/)

## AI Instructions

When using Azure:
1. Set billing alerts.
2. Use managed services (App Service, SQL Database, etc.).
3. Use Entra ID (formerly Azure AD) for auth.
4. Use IaC (Bicep, Terraform).
5. Multi-region for HA.
6. Use Azure Front Door for CDN/WAF.

## Human Notes

### Core services
- **VMs** — Virtual Machines.
- **App Service** — PaaS web hosting.
- **Functions** — serverless.
- **Container Apps** — serverless containers.
- **AKS** — managed Kubernetes.
- **Blob Storage** — object storage.
- **SQL Database** — managed SQL Server.
- **Cosmos DB** — multi-model NoSQL.
- **PostgreSQL / MySQL** — managed.
- **Cache for Redis** — managed Redis.
- **Front Door** — CDN + WAF + LB.
- **Traffic Manager** — DNS LB.
- **Key Vault** — secrets / keys / certs.
- **Application Insights** — APM.
- **Service Bus** — queue / pub-sub.
- **Event Hubs** — streaming.
- **Event Grid** — event routing.
- **Cognitive Services** — AI APIs.
- **OpenAI Service** — managed OpenAI.

### CLI
```bash
az login
az group create --name mygroup --location eastus
az appservice plan create ...
az webapp create ...
az storage account create ...
```

### IaC
- **Bicep** — Azure-native, declarative.
- **Terraform** — multi-cloud.
- **ARM templates** — verbose JSON (legacy).

### When to use Azure
- Enterprise on Microsoft stack.
- .NET apps.
- Existing Microsoft licensing (Enterprise Agreement).
- Active Directory integration.

### When NOT to use
- Cost-sensitive startups (AWS/GCP often cheaper).
- Multi-cloud (avoid lock-in).
- Heavy Linux / OSS stack.

## Common Mistakes

- ❌ No billing alerts.
- ❌ Wrong region.
- ❌ Open NSGs.
- ❌ Secrets in code.
- ❌ Single region.

## Tools

- Azure docs: https://learn.microsoft.com/azure
- Azure CLI: https://learn.microsoft.com/cli/azure
- Bicep: https://learn.microsoft.com/azure/azure-resource-manager/bicep/
- Azure Portal: https://portal.azure.com/

## References

- Azure Architecture Center: https://learn.microsoft.com/azure/architecture/

## Exercises

1. Deploy a .NET app to App Service.
2. Set up Azure SQL + Key Vault.
3. Build a serverless function.

## Projects

- Build an enterprise app on Azure with Entra ID auth.

---

**Previous:** [AWS/](../AWS/) · **Next:** [GCP/](../GCP/) · **Related:** [Cloud/](../Cloud/)
