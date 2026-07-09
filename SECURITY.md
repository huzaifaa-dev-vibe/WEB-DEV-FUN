# SECURITY

> Threat model, security policy, and security best-practice index for this repository.

This file is the security policy for the WEB-DEV-FUN repo itself, plus the master index for security topics across the repository. For deep security guidance, see the [Security/](Security/) folder.

---

## Reporting a Vulnerability in This Repo

If you find a security issue with the WEB-DEV-FUN repository itself (e.g., a malicious link, leaked secret in examples, code that teaches an insecure pattern):

1. **Do NOT open a public issue.**
2. Email: `security@your-org.example` (replace with real address when forked).
3. Include: description, repro, impact, suggested fix.
4. We will respond within 72 hours and disclose responsibly after a fix.

---

## Threat Model (for projects built using this repo)

This repository is a knowledge base. It does not run code in production. The threats to consider are:

| Threat | Mitigation |
|---|---|
| Code samples contain insecure patterns | Every code sample reviewed; security folder flags common pitfalls |
| External links rot or get hijacked | Links checked periodically; pinned where possible |
| Examples accidentally leak secrets | Examples use placeholders only; no real keys |
| AI agents following this repo produce insecure code | [AI_AGENT_GUIDE.md](AI_AGENT_GUIDE.md) requires verification steps; security checklist mandatory |

---

## Security Topics Index

| Topic | File |
|---|---|
| OWASP Top 10 | [Security/owasp.md](Security/owasp.md) |
| HTTP security headers | [Security/headers.md](Security/headers.md) |
| HTTPS / TLS / HSTS | [Security/https.md](Security/https.md) |
| CORS | [Security/cors.md](Security/cors.md) |
| CSP | [Security/headers.md#csp](Security/headers.md) |
| CSRF | [Security/csrf.md](Security/csrf.md) |
| XSS | [Security/xss.md](Security/xss.md) |
| SQL Injection | [Security/sql-injection.md](Security/sql-injection.md) |
| SSRF | [Security/ssrf.md](Security/ssrf.md) |
| Rate limiting | [Security/rate-limiting.md](Security/rate-limiting.md) |
| Passwords (hashing) | [Security/passwords.md](Security/passwords.md) |
| Session management | [Security/sessions.md](Security/sessions.md) |
| JWT | [Security/jwt.md](Security/jwt.md) |
| OAuth | [Security/oauth.md](Security/oauth.md) |
| Passkeys / WebAuthn | [Security/passkeys.md](Security/passkeys.md) |
| Secrets management | [Security/secrets.md](Security/secrets.md) |
| Supply chain (deps) | [Security/supply-chain.md](Security/supply-chain.md) |
| Threat modeling | [Security/threat-modeling.md](Security/threat-modeling.md) |
| AI / LLM security | [Security/ai.md](Security/ai.md) |
| Logging & PII | [Logging/redaction.md](Logging/redaction.md) |

→ [Authentication/](Authentication/) for auth flows.
→ [SECURITY.md](SECURITY.md) (this file) for policy.

---

## Security Checklist (minimum bar)

Before any code ships:

- [ ] HTTPS enforced, HSTS header set
- [ ] CSP header set (strict, nonces or hashes)
- [ ] X-Content-Type-Options: nosniff
- [ ] X-Frame-Options: DENY or frame-ancestors in CSP
- [ ] Referrer-Policy set
- [ ] Permissions-Policy set
- [ ] CORS allowlist (never `*` with credentials)
- [ ] All inputs validated (Zod/Valibot)
- [ ] All SQL parameterized
- [ ] No secrets in code
- [ ] Passwords hashed (bcrypt/argon2)
- [ ] Auth tokens: short TTL, refresh rotation
- [ ] Rate limiting on auth + write endpoints
- [ ] CSRF protection (if cookie-based)
- [ ] Dependency audit (`npm audit`, Snyk, Dependabot)
- [ ] Logs don't contain PII/secrets
- [ ] Error messages don't leak internals
- [ ] Admin endpoints behind authz checks
- [ ] File uploads validated (type, size, content)
- [ ] Outbound requests validated (SSRF)

→ [Checklists/pre-launch.md](Checklists/pre-launch.md) for the full pre-launch checklist.

---

**Next:** [Security/](Security/) · [Authentication/](Authentication/) · [Checklists/](Checklists/)
