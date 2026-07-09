# Security Checklist

> Run on every auth/security-related change. Run before launch.

## Transport
- [ ] HTTPS enforced.
- [ ] HSTS header set (`max-age=31536000; includeSubDomains; preload`).
- [ ] No mixed content.
- [ ] TLS 1.2+ only.
- [ ] Cert auto-renewing.

## Headers
- [ ] `Content-Security-Policy` strict (nonces or hashes).
- [ ] `X-Content-Type-Options: nosniff`.
- [ ] `X-Frame-Options: DENY` or `frame-ancestors` in CSP.
- [ ] `Referrer-Policy: strict-origin-when-cross-origin`.
- [ ] `Permissions-Policy` set.
- [ ] `Cross-Origin-Opener-Policy: same-origin`.
- [ ] `Cross-Origin-Embedder-Policy: require-corp`.
- [ ] `Cross-Origin-Resource-Policy: same-origin`.

## Auth
- [ ] Passwords hashed (bcrypt cost 12+ or argon2id).
- [ ] No plaintext passwords.
- [ ] JWT TTL short (< 15 min).
- [ ] Refresh token rotation.
- [ ] JWT not in localStorage (HttpOnly cookie preferred).
- [ ] MFA available.
- [ ] Email verification required.
- [ ] Password reset token: 1h expiry, one-time use.
- [ ] Rate limit login (per IP + per user).
- [ ] Lockout after N failed attempts.

## Authorization
- [ ] Server enforces all authz (not client).
- [ ] Per-resource ownership checks.
- [ ] Admin endpoints behind RBAC.
- [ ] Multi-tenant: row-level security or scoped queries.

## Input Validation
- [ ] All inputs validated (Zod / Valibot).
- [ ] All SQL parameterized.
- [ ] No `eval` / `Function()` / `innerHTML` with user input.
- [ ] Sanitize HTML (DOMPurify).
- [ ] File uploads: type, size, content validated.
- [ ] URL inputs checked for SSRF.

## CORS
- [ ] Allowlist specific origins.
- [ ] No `*` with credentials.
- [ ] `Access-Control-Allow-Credentials: true` only when needed.

## CSRF
- [ ] CSRF tokens for cookie-based auth.
- [ ] `SameSite=Lax` or `Strict` on cookies.

## Rate Limiting
- [ ] On auth endpoints.
- [ ] On write endpoints.
- [ ] On public endpoints.
- [ ] Per IP + per user.

## Secrets
- [ ] No secrets in code.
- [ ] No secrets in env of client bundles.
- [ ] Secrets in vault / CI secrets.
- [ ] Secret rotation plan.

## Dependencies
- [ ] `npm audit` clean.
- [ ] Dependabot / Snyk enabled.
- [ ] No critical vulnerabilities.
- [ ] Lockfile committed.
- [ ] Pinned versions.

## Logging
- [ ] No PII in logs.
- [ ] No secrets in logs.
- [ ] Auth events logged (login, logout, failed).
- [ ] Audit log for sensitive operations.
- [ ] Logs shipped to aggregator.

## Errors
- [ ] Error messages don't leak internals.
- [ ] Stack traces hidden in prod.
- [ ] 500 page generic.

## Supply Chain
- [ ] Lockfile in git.
- [ ] Pin actions by SHA.
- [ ] Verify package integrity.
- [ ] Review new deps.

## AI (if applicable)
- [ ] Prompt injection defenses.
- [ ] Output validated.
- [ ] Per-user cost limits.
- [ ] No PII sent to LLM provider.

## Audit
- [ ] OWASP Top 10 reviewed.
- [ ] securityheaders.com A+.
- [ ] SSL Labs A+.
- [ ] Mozilla Observatory A+.
- [ ] Trivy scan on Docker images.
- [ ] Manual pentest (if high-stakes).

---

**Next:** [seo.md](seo.md) · Back to [Checklists/](README.md)
