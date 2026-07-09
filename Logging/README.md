# Logging

> Structured logs with correlation IDs. For debugging and auditing.

---

## Purpose

Implement structured logging that scales with your system.

## Prerequisites

- [Backend/](../Backend/).

## Learning Outcome

You can ship logs that are useful for debugging, audits, and analytics.

## Dependencies

- A log aggregator.

## Related Files

- [Monitoring/](../Monitoring/) · [DEBUGGING.md](../DEBUGGING.md) · [Logging/redaction.md](redaction.md)

## AI Instructions

When logging:
1. **Structured** (JSON).
2. **Levels** (debug, info, warn, error).
3. **Request ID** for correlation.
4. **Trace ID** for OpenTelemetry.
5. **No PII** or secrets.
6. **Don't `console.log`** in production code.
7. Use **Pino** (Node), **structlog** (Python), **zerolog** (Go).

## Human Notes

### Why structured logs
```js
// BAD
console.log(`User ${userId} logged in from ${ip}`);

// GOOD
logger.info({ event: 'user_logged_in', userId, ip, ts: Date.now() });
```
- Searchable.
- Aggregatable.
- Filterable.

### Levels
- **debug** — verbose, off in prod.
- **info** — normal events (user signed up).
- **warn** — degraded but functional.
- **error** — failed operation.
- **fatal** — process must exit.

### What to log
- Auth events (login, logout, failed).
- Authorization events (denied access).
- State changes (user updated, post deleted).
- Errors with stack traces.
- Slow operations.
- Business events (payment received).

### What NOT to log
- Passwords.
- Tokens / secrets.
- PII (SSN, credit card, health info).
- Full request bodies (may contain PII).
- High-frequency noise (per-pixel mouse moves).

### Correlation
- Generate request ID at edge.
- Pass through all services.
- Include in every log.

```js
app.use((req, res, next) => {
  req.id = req.headers['x-request-id'] || crypto.randomUUID();
  logger.info({ event: 'request', id: req.id, method: req.method, path: req.path });
  next();
});
```

### Sampling
For high-volume logs (e.g., per-request metrics), sample:
- Log 1% of successful requests.
- Log 100% of errors.

### Log aggregation
- **Loki** — open-source, integrates with Grafana.
- **Datadog** — commercial.
- **Splunk** — enterprise.
- **Axiom** — serverless-friendly.
- **CloudWatch** (AWS), **Stackdriver** (GCP), **Log Analytics** (Azure).
- **Highlight.io** — open-source.

### Pino (Node)
```js
import pino from 'pino';
const logger = pino({
  level: process.env.LOG_LEVEL || 'info',
  redact: ['password', '*.token', '*.ssn'],
});

logger.info({ event: 'user_created', userId: 1 });
logger.error({ err, userId: 1 }, 'failed to send email');
```

### Search
- Loki: LogQL.
- Datadog: Lucene-like.
- Splunk: SPL.

### Retention
- Hot (searchable): 7-30 days.
- Warm (slower): 90 days.
- Cold (archive): 1-7 years for compliance.

## Common Mistakes

- ❌ `console.log` in prod.
- ❌ Unstructured logs.
- ❌ No correlation IDs.
- ❌ PII in logs.
- ❌ Logging too much (noise).
- ❌ Logging too little (can't debug).
- ❌ No retention policy.

## Tools

- Pino: https://github.com/pinojs/pino
- Winston: https://github.com/winstonjs/winston
- structlog (Python): https://www.structlog.org/
- zerolog (Go): https://github.com/rs/zerolog
- tracing (Rust): https://github.com/tokio-rs/tracing
- Loki: https://grafana.com/oss/loki/
- Axiom: https://axiom.co/

## References

- 12-factor logs: https://12factor.net/logs

## Exercises

1. Add Pino to a Node app. Add request IDs.
2. Set up Loki + Grafana.
3. Add log redaction.

## Projects

- Build a log pipeline (app → fluent-bit → Loki → Grafana).

---

**Previous:** [Monitoring/](../Monitoring/) · **Next:** [Security/](../Security/) · **Related:** [Backend/](../Backend/)
