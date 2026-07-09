# Security

> OWASP Top 10. Headers, secrets, auth, encryption, supply chain.

---

## Purpose

Secure web apps against common threats.

## Prerequisites

- [Backend/](../Backend/), [Authentication/](../Authentication/).

## Learning Outcome

You can audit, harden, and operate a secure web app.

## Dependencies

- None (conceptual).

## Related Files

- [SECURITY.md](../SECURITY.md) · [Authentication/](../Authentication/) · [Security/owasp.md](owasp.md) · [Security/headers.md](headers.md) · [Security/cors.md](cors.md) · [Security/csrf.md](csrf.md) · [Security/xss.md](xss.md) · [Security/sql-injection.md](sql-injection.md) · [Security/ssrf.md](ssrf.md) · [Security/secrets.md](secrets.md) · [Security/passwords.md](passwords.md) · [Security/ai.md](ai.md)

## AI Instructions

When building secure apps:
1. **HTTPS everywhere.** HSTS.
2. **CSP** strict (nonces/hashes).
3. **CORS** allowlist (never `*` with credentials).
4. **Validate all input** (Zod).
5. **Parameterize SQL.**
6. **Hash passwords** (bcrypt/argon2).
7. **Rate limit** auth + write endpoints.
8. **Secrets in vault.**
9. **CSRF protection** for cookies.
10. **OWASP Top 10** audit.
11. **Dependency audit** (Dependabot, Snyk).
12. **No PII in logs.**

## Human Notes

### OWASP Top 10 (2021)
1. Broken Access Control.
2. Cryptographic Failures.
3. Injection (SQL, NoSQL, OS, LDAP).
4. Insecure Design.
5. Security Misconfiguration.
6. Vulnerable and Outdated Components.
7. Identification and Authentication Failures.
8. Software and Data Integrity Failures.
9. Security Logging and Monitoring Failures.
10. Server-Side Request Forgery (SSRF).

→ [Security/owasp.md](owasp.md)

### Security headers
```http
Strict-Transport-Security: max-age=31536000; includeSubDomains; preload
Content-Security-Policy: default-src 'self'; script-src 'self' 'nonce-abc'
X-Content-Type-Options: nosniff
X-Frame-Options: DENY
Referrer-Policy: strict-origin-when-cross-origin
Permissions-Policy: geolocation=(), microphone=(), camera=()
Cross-Origin-Opener-Policy: same-origin
Cross-Origin-Embedder-Policy: require-corp
Cross-Origin-Resource-Policy: same-origin
```
→ [Security/headers.md](headers.md)

Use `helmet` (Node) or framework equivalent.

### CORS
- Allowlist origins.
- `Access-Control-Allow-Origin: *` with credentials = security hole.
- → [Security/cors.md](cors.md)

### CSRF
- Cookie-based auth = vulnerable to CSRF.
- Token-based (JWT in header) = not vulnerable.
- → [Security/csrf.md](csrf.md)

### XSS
- User input rendered as HTML = XSS.
- Use `textContent` not `innerHTML`.
- Sanitize with DOMPurify if you must.
- CSP for defense in depth.
- → [Security/xss.md](xss.md)

### SQL Injection
- Use parameterized queries.
- Never string-concat SQL.
- → [Security/sql-injection.md](sql-injection.md)

### SSRF
- User-supplied URLs fetched server-side = SSRF risk.
- Validate/allowlist.
- → [Security/ssrf.md](ssrf.md)

### Passwords
- bcrypt (cost 12+) or argon2id.
- Never store plaintext.
- Never MD5/SHA1.
- → [Security/passwords.md](passwords.md)

### Secrets
- Env vars / vault.
- Never in code / git.
- Rotate.
- → [Security/secrets.md](secrets.md)

### Rate limiting
- Per IP + per user.
- Stricter on auth endpoints.
- → [Security/rate-limiting.md](rate-limiting.md)

### Auth
- → [Authentication/](../Authentication/)

### Supply chain
- Lockfile.
- `npm audit` / Snyk / Dependabot.
- Sigstore / cosign for signed packages.
- Pin versions.
- Review new deps.

### Encryption
- At rest: DB encryption, S3 SSE.
- In transit: TLS 1.2+.
- Don't roll your own crypto.
- Use vetted libs (crypto module, libsodium).

### AI security
- Prompt injection.
- Output validation.
- Cost attacks.
- Data exfiltration.
- → [Security/ai.md](ai.md)

### Incident response
1. Detect.
2. Contain.
3. Eradicate.
4. Recover.
5. Post-mortem.
→ [Checklists/post-mortem.md](../Checklists/post-mortem.md)

### Security audit checklist
- [ ] OWASP Top 10 audit.
- [ ] Security headers (A+ on securityheaders.com).
- [ ] CORS allowlist.
- [ ] All inputs validated.
- [ ] SQL parameterized.
- [ ] Passwords hashed.
- [ ] Secrets in vault.
- [ ] Rate limiting on auth.
- [ ] CSRF protection.
- [ ] HTTPS + HSTS.
- [ ] Dependency audit.
- [ ] No PII in logs.
- [ ] WAF for public apps.
- [ ] Backups encrypted.
- [ ] 2FA for admins.
- [ ] Audit logs.

## Common Mistakes

- ❌ HTTP (not HTTPS).
- ❌ `*` CORS with credentials.
- ❌ Plaintext passwords.
- ❌ String-concat SQL.
- ❌ Secrets in code.
- ❌ No rate limiting.
- ❌ No CSRF protection.
- ❌ No security headers.
- ❌ Trusting client input.
- ❌ No dep audits.

## Tools

- OWASP ZAP: https://www.zaproxy.org/
- Burp Suite: https://portswigger.net/burp
- Snyk: https://snyk.io/
- Dependabot: GitHub-native.
- securityheaders.com: https://securityheaders.com/
- SSL Labs: https://www.ssllabs.com/ssltest/
- Mozilla Observatory: https://observatory.mozilla.org/
- Trivy: https://github.com/aquasecurity/trivy
- git-secrets: https://github.com/awslabs/git-secrets
- Sigstore: https://www.sigstore.dev/

## References

- OWASP: https://owasp.org/
- OWASP Cheat Sheets: https://cheatsheetseries.owasp.org/
- Web Security Academy (free): https://portswigger.net/web-security
- auth0 security: https://auth0.com/security

## Further Reading

- *The Web Application Hacker's Handbook* — Stuttard, Pinto
- *Threat Modeling* — Adam Shostick
- *Real-World Cryptography* — David Wong

## Exercises

1. Audit your app against OWASP Top 10.
2. Get A+ on securityheaders.com.
3. Run `npm audit` and fix all issues.
4. Run OWASP ZAP against your app.

## Projects

- Build a secure auth system (OWASP-compliant).

---

**Previous:** [Logging/](../Logging/) · **Next:** [Clean-Code/](../Clean-Code/) · **Related:** [Authentication/](../Authentication/)
