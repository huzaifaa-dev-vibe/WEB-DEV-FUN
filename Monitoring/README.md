# Monitoring

> If you can't see it, you can't fix it. Logs, metrics, traces, alerts.

---

## Purpose

Set up observability: metrics, logs, traces, alerts, dashboards.

## Prerequisites

- [Backend/](../Backend/), [Deployment/](../Deployment/).

## Learning Outcome

You can instrument an app, set up dashboards and alerts, and operate with confidence.

## Dependencies

- A monitoring stack.

## Related Files

- [Logging/](../Logging/) · [Performance/](../Performance/) · [DEBUGGING.md](../DEBUGGING.md) · [Checklists/post-mortem.md](../Checklists/post-mortem.md) · [EXTERNAL_REPOSITORIES.md#monitoring--observability](../EXTERNAL_REPOSITORIES.md#monitoring--observability)

## AI Instructions

When setting up monitoring:
1. **Logs** (what happened).
2. **Metrics** (numbers over time).
3. **Traces** (request flow across services).
4. **Alerts** (page on user-facing symptoms).
5. **Dashboards** (SLOs, not vanity).
6. **Runbooks** for every alert.

## Human Notes

### Three pillars of observability
1. **Logs** — discrete events. For debugging.
2. **Metrics** — numeric over time. For alerting + dashboards.
3. **Traces** — request flow. For understanding.

Plus: **profiles** (CPU/memory), **events** (deploys, incidents).

### SLO / SLI / SLA
- **SLI** — Service Level Indicator (e.g., 99.9% of requests < 200ms).
- **SLO** — Service Level Objective (target, e.g., 99.9% over 30 days).
- **SLA** — Service Level Agreement (contract with customers).
- **Error budget** = 1 - SLO. Burn rate alerts when consuming too fast.

### Symptoms vs causes
- Alert on **symptoms** (user-visible issues).
- Debug from **causes**.
- e.g., "high latency" is a symptom. "DB CPU 100%" is a cause.

### Metrics
- **Counter** — monotonically increasing (requests_total).
- **Gauge** — up/down (queue_depth).
- **Histogram** — distribution (request_duration).
- **Summary** — quantiles (less common now).

Use OpenTelemetry for instrumentation.

### Logs
- Structured (JSON).
- Include request ID, user ID, trace ID.
- Levels: debug, info, warn, error.
- Don't log PII/secrets.
- → [Logging/](../Logging/)

### Traces
- One trace per request.
- Spans for sub-operations.
- OpenTelemetry standard.
- Distributed across services.

### Alerts
- Page on user-facing symptoms (latency, error rate, availability).
- Warn on causes (CPU, disk, queue depth).
- Don't alert on individual log lines (use patterns).
- Don't alert on things you can't act on.

### Dashboards
- SLO dashboard (top).
- Service dashboard (per service).
- Resource dashboard (infra).
- Runbook links.

### Tools
- **OpenTelemetry** — instrumentation standard.
- **Prometheus** — metrics.
- **Grafana** — dashboards.
- **Loki** — logs.
- **Tempo / Jaeger** — traces.
- **Sentry** — errors.
- **Datadog / New Relic** — commercial all-in-one.
- **Highlight.io** — open-source full-stack observability.
- **Axiom** — logs.
- **BetterStack** — uptime + logs.

### APM (Application Performance Monitoring)
- Sentry, Datadog, New Relic, AppDynamics.
- Errors + perf + traces.

### Synthetic monitoring
- Hit endpoints from outside, alert on failure.
- BetterStack, Checkly, UptimeRobot.

### RUM (Real User Monitoring)
- Collect perf from real users.
- `web-vitals` library + beacon.

## Common Mistakes

- ❌ Alert fatigue (too many low-signal alerts).
- ❌ Vanity dashboards (no SLOs).
- ❌ Logs without structure or correlation IDs.
- ❌ No traces (can't debug distributed systems).
- ❌ No runbooks.
- ❌ Alerting on causes, not symptoms.
- ❌ Logging PII.

## Tools

- OpenTelemetry: https://opentelemetry.io/
- Prometheus: https://prometheus.io/
- Grafana: https://grafana.com/
- Loki: https://grafana.com/oss/loki/
- Tempo: https://grafana.com/oss/tempo/
- Sentry: https://sentry.io/
- Highlight.io: https://www.highlight.io/

## References

- Google SRE book (free): https://sre.google/sre-book/table-of-contents/
- OpenTelemetry docs: https://opentelemetry.io/docs/
- Honeycomb blog: https://www.honeycomb.io/blog

## Further Reading

- *Observability Engineering* — Charity Majors, Liz Fong-Jones, George Miranda
- *Site Reliability Engineering* — Google (free)
- *SRE Workbook* — Google (free)

## Exercises

1. Instrument an app with OpenTelemetry (logs + metrics + traces).
2. Set up a Grafana dashboard.
3. Define an SLO + alert.

## Projects

- Build a monitoring stack (Prometheus + Grafana + Loki + Tempo).

---

**Previous:** [GCP/](../GCP/) · **Next:** [Logging/](../Logging/) · **Related:** [Performance/](../Performance/)
