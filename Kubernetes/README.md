# Kubernetes

> Container orchestration. Scale, heal, deploy containerized apps.

---

## Purpose

Master K8s: pods, deployments, services, ingress, config, secrets, operators.

## Prerequisites

- [Docker/](../Docker/), [Linux/](../Linux/), [Deployment/](../Deployment/).

## Learning Outcome

You can deploy, scale, and operate a K8s cluster.

## Dependencies

- A K8s cluster (managed: EKS/GKE/AKS; or local: kind, minikube).

## Related Files

- [Docker/](../Docker/) · [Deployment/](../Deployment/) · [CI-CD/](../CI-CD/) · [Cloud/](../Cloud/) · [AWS/](../AWS/) · [GCP/](../GCP/) · [Azure/](../Azure/)

## AI Instructions

When using K8s:
1. **Use managed K8s** (EKS/GKE/AKS) — don't self-host control plane.
2. **Helm** for packaging.
3. **GitOps** (Argo CD / Flux) for deploys.
4. **Ingress** (nginx-ingress, Traefik, ALB).
5. **cert-manager** for TLS.
6. **ExternalDNS** for DNS.
7. **HorizontalPodAutoscaler** for scale.
8. **PodDisruptionBudget** for HA.
9. **Probes** (liveness, readiness, startup).
10. **Resource requests/limits** on every pod.

## Human Notes

### When to use K8s
- Multiple services / microservices.
- Multiple teams.
- Need to scale horizontally.
- Need advanced deploy strategies (canary, blue-green).
- Already have K8s expertise.

### When NOT to use K8s
- Single service → use Vercel, Cloud Run, Fly.io.
- Small team without K8s expertise.
- Startup in MVP phase.
- "I want to learn K8s" on a production app.

### Core concepts
- **Pod** — smallest unit, 1+ containers.
- **Deployment** — manages replicas of pods.
- **Service** — stable network endpoint for pods.
- **Ingress** — HTTP routing.
- **ConfigMap** — non-secret config.
- **Secret** — secret config.
- **PersistentVolume** — storage.
- **StatefulSet** — for stateful apps (DBs).
- **Job / CronJob** — batch / scheduled.
- **Namespace** — logical grouping.

### Hello Deployment
```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: myapp
spec:
  replicas: 3
  selector:
    matchLabels: { app: myapp }
  template:
    metadata:
      labels: { app: myapp }
    spec:
      containers:
      - name: myapp
        image: myapp:1.0.0
        ports: [{ containerPort: 3000 }]
        resources:
          requests: { cpu: 100m, memory: 128Mi }
          limits: { cpu: 500m, memory: 256Mi }
        livenessProbe:
          httpGet: { path: /health, port: 3000 }
          initialDelaySeconds: 10
        readinessProbe:
          httpGet: { path: /ready, port: 3000 }
        env:
        - name: DATABASE_URL
          valueFrom:
            secretKeyRef: { name: app-secrets, key: database-url }
---
apiVersion: v1
kind: Service
metadata:
  name: myapp
spec:
  selector: { app: myapp }
  ports: [{ port: 80, targetPort: 3000 }]
---
apiVersion: networking.k8s.io/v1
kind: Ingress
metadata:
  name: myapp
  annotations:
    cert-manager.io/cluster-issuer: letsencrypt
spec:
  tls:
  - hosts: [myapp.example.com]
    secretName: myapp-tls
  rules:
  - host: myapp.example.com
    http:
      paths:
      - path: /
        pathType: Prefix
        backend:
          service:
            name: myapp
            port: { number: 80 }
```

### kubectl cheatsheet
```bash
kubectl get pods
kubectl get deployments
kubectl get svc
kubectl get ingress
kubectl describe pod <name>
kubectl logs <pod>
kubectl logs -f <pod>
kubectl exec -it <pod> -- sh
kubectl apply -f manifest.yaml
kubectl delete -f manifest.yaml
kubectl scale deployment myapp --replicas=5
kubectl rollout restart deployment myapp
kubectl rollout undo deployment myapp
kubectl get events --sort-by='.lastTimestamp'
```

### Helm
Package manager for K8s.
```bash
helm repo add bitnami https://charts.bitnami.com/bitnami
helm install my-release bitnami/postgresql
```

### GitOps (Argo CD)
- Declarative.
- Git is source of truth.
- Auto-sync.
- Audit trail.

### Autoscaling
- HPA (Horizontal Pod Autoscaler) — scale by CPU/mem/custom.
- VPA (Vertical Pod Autoscaler) — adjust requests.
- Cluster Autoscaler — add nodes.

### Storage
- PersistentVolume + PersistentVolumeClaim.
- StorageClass for dynamic provisioning.
- StatefulSet for stateful workloads (DBs).

### Networking
- CNI (Calico, Cilium, Flannel).
- Service mesh (Istio, Linkerd) — mTLS, traffic control.
- Ingress controller (nginx, Traefik, ALB).

### Security
- RBAC.
- Network policies.
- Pod security standards.
- Image scanning (Trivy, Snyk).
- Secrets encryption at rest.

### Observability
- Logs: Loki + Grafana.
- Metrics: Prometheus + Grafana.
- Traces: Tempo / Jaeger.
- Or use managed: Datadog, NewRelic.

## Common Mistakes

- ❌ No resource requests/limits (noisy neighbor, OOM kills).
- ❌ No probes.
- ❌ Latest tag.
- ❌ Too many namespaces.
- ❌ Self-hosted control plane (use managed).
- ❌ Running DBs on K8s without expertise.
- ❌ No PodDisruptionBudget (disruptions during upgrades).

## Tools

- kubectl: https://kubernetes.io/docs/reference/kubectl/
- k9s (TUI): https://k9scli.io/
- Lens (GUI): https://k8slens.dev/
- Helm: https://helm.sh/
- Argo CD: https://argoproj.github.io/argo-cd/
- Flux: https://fluxcd.io/
- kind / minikube (local): https://kind.sigs.k8s.io/
- kubectx / kubens: https://github.com/ahmetb/kubectx
- stern (multi-pod logs): https://github.com/stern/stern

## References

- K8s docs: https://kubernetes.io/docs/
- K8s Patterns: https://www.redhat.com/en/resources/oreilly-kubernetes-patterns-cloud-native-apps
- Awesome Kubernetes: https://github.com/ramitsurana/awesome-kubernetes

## Further Reading

- *Kubernetes Up and Running* — Brendan Burns et al.
- *Production Kubernetes* — Josh Rosso et al.

## Exercises

1. Run a local cluster with kind. Deploy a Node app.
2. Add Ingress + TLS with cert-manager.
3. Set up HPA.

## Projects

- Build a GitOps pipeline with Argo CD.

---

**Previous:** [Docker/](../Docker/) · **Next:** [CI-CD/](../CI-CD/) · **Related:** [Deployment/](../Deployment/)
