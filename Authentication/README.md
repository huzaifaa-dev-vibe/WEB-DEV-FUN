# Authentication

> Who are you? Prove it. Now what can you do?

---

## Purpose

Implement secure authentication (authn) and authorization (authz) for web apps.

## Prerequisites

- [Backend/](../Backend/) basics, [Security/](../Security/).

## Learning Outcome

You can pick the right auth model, implement it securely, and avoid common pitfalls.

## Dependencies

- Backend framework.

## Related Files

- [Security/](../Security/) · [Authentication/flows.md](flows.md) · [Authentication/oauth.md](oauth.md) · [Authentication/jwt.md](jwt.md) · [Authentication/passkeys.md](passkeys.md) · [EXTERNAL_REPOSITORIES.md#authentication](../EXTERNAL_REPOSITORIES.md#authentication)

## AI Instructions

When implementing auth:
1. **Don't roll your own crypto.** Use vetted libraries.
2. **Don't store plaintext passwords.** bcrypt/argon2.
3. **JWT**: short TTL, refresh token rotation, don't store in localStorage.
4. **Sessions**: HttpOnly cookies, SameSite=Lax/Strict, CSRF tokens.
5. **OAuth**: use a library (`openid-client`), don't hand-roll.
6. **Passkeys**: future-proof. Consider for new apps.
7. **Rate limit** auth endpoints.
8. **MFA** for sensitive operations.
9. **Audit log** auth events.
10. **Test** all flows (signup, login, logout, reset, verify, MFA).

## Decision Tree

```
Building a SaaS?
├─ B2C, simple → Clerk / Auth0 / Supabase Auth
├─ B2C, custom → Better-Auth / Lucia / NextAuth
├─ B2B, enterprise SSO → WorkOS / Auth0 / Ory
└─ Internal → simple sessions

Cookie-based (session) or token-based (JWT)?
├─ Web app with server → sessions (HttpOnly cookies)
├─ Mobile / 3rd-party API → JWT
└─ Both → sessions for web, JWT for API

Want to add social login?
├─ Use NextAuth/Auth.js (React/Next)
├─ Use OAuth libraries (Node: `openid-client`)
└─ Use managed: Clerk, Auth0, Supabase

Want passwordless?
├─ Magic link (email)
├─ OTP (SMS / email)
├─ Passkeys (WebAuthn) — future-proof
└─ Use: Clerk, Stytch, Passage, Better-Auth
```

## Human Notes

### Authn vs Authz
- **Authn** (authentication) — who are you?
- **Authz** (authorization) — what can you do?

Both required. Don't conflate.

### Session-based auth
```
1. User logs in with email + password.
2. Server validates, creates session in DB.
3. Server sends session ID in HttpOnly cookie.
4. On every request, cookie sent automatically.
5. Server validates session, attaches user to request.
6. On logout, delete session.
```

Pros: simple, secure-by-default, easy to revoke.
Cons: needs session store, doesn't scale to many servers easily (use shared store like Redis).

### JWT-based auth
```
1. User logs in.
2. Server signs JWT with secret, returns to client.
3. Client stores JWT (memory or HttpOnly cookie).
4. Client sends JWT in Authorization header.
5. Server verifies signature, extracts user.
6. Token expires; refresh with refresh token.
```

Pros: stateless, scales horizontally, works across domains.
Cons: revocation hard (need blocklist), token leak = impersonation, larger payload.

**Don't put JWT in localStorage.** XSS steals it. Use HttpOnly cookies.

### OAuth 2.0
For "Log in with Google/GitHub/etc."

Flows:
- **Authorization Code + PKCE** — for SPAs and mobile.
- **Client Credentials** — for server-to-server.
- **Device Code** — for TVs, IoT.

→ [Authentication/oauth.md](oauth.md)

### OIDC (OpenID Connect)
Built on OAuth 2.0. Adds identity layer (ID token with user info). Use this for "log in with X".

### Passkeys (WebAuthn)
- Passwordless, phishing-resistant.
- Uses device biometrics (Face ID, Touch ID, Windows Hello).
- Future of auth.
- Library: `@simplewebauthus/server` + `@simplewebauthus/browser`.
- Or use: Clerk, Stytch, Passage.

→ [Authentication/passkeys.md](passkeys.md)

### MFA (Multi-Factor Auth)
- TOTP (Google Authenticator, Authy) — `otplib`.
- SMS (less secure, but usable).
- Hardware keys (YubiKey) — WebAuthn.
- Email OTP.

For sensitive apps, mandate MFA.

### Password storage
- **bcrypt** — battle-tested. Cost factor 12+.
- **argon2id** — modern, recommended. Memory-hard.
- **NEVER MD5/SHA1/plain.**

```js
import bcrypt from 'bcrypt';
const hash = await bcrypt.hash(password, 12);
const valid = await bcrypt.compare(input, hash);
```

### Email verification
- Send token via email.
- Token expires in 24h.
- One-time use.
- Rate limit resends.

### Password reset
- Send token via email.
- Token expires in 1h.
- One-time use.
- Invalidate all sessions after reset.
- Notify user via email after reset.

### Session management
- Generate with `crypto.randomUUID()` or random bytes.
- Store hash in DB (not the session ID itself).
- Set HttpOnly, Secure, SameSite=Lax cookies.
- Set reasonable expiry (30 days for "remember me", 1 day otherwise).
- Rotate on privilege change (login, MFA enable).
- Allow revoking sessions (logout everywhere).

### CSRF protection
- For cookie-based auth.
- Use CSRF tokens (double-submit or synchronizer token).
- Set `SameSite=Lax` (default in modern browsers).
- → [Security/csrf.md](../Security/csrf.md)

### Authorization patterns
- **RBAC** (Role-Based Access Control) — user has role, role has permissions.
- **ABAC** (Attribute-Based) — fine-grained, based on attributes.
- **ReBAC** (Relationship-Based) — Google Zanzibar / SpiceDB / Ory Keto.

Server enforces, not client.

### Common mistakes
- ❌ Plaintext passwords.
- ❌ JWT in localStorage.
- ❌ No rate limiting on login.
- ❌ No CSRF protection (cookie auth).
- ❌ Weak password requirements (or too strict).
- ❌ Email verification optional.
- ❌ Password reset token reuse.
- ❌ No session expiry.
- ❌ Client-side authz enforcement only.
- ❌ Logging passwords/secrets.

→ [COMMON_MISTAKES.md#backend](../COMMON_MISTAKES.md), [Security/](../Security/)

## Libraries & Services

→ [EXTERNAL_REPOSITORIES.md#authentication](../EXTERNAL_REPOSITORIES.md#authentication)

Highlights:
- **NextAuth/Auth.js** — Next.js default.
- **Better-Auth** — modern TS auth library.
- **Lucia** — simple, flexible.
- **Clerk** — managed, beautiful UI.
- **Auth0** — managed, enterprise.
- **Supabase Auth** — built into Supabase.
- **WorkOS** — enterprise SSO.
- **Stytch** — passwordless.
- **Passage (1Password)** — passkeys.

## References

- OWASP Auth Cheat Sheet: https://cheatsheetseries.owasp.org/cheatsheets/Authentication_Cheat_Sheet.html
- WebAuthn guide: https://webauthn.guide/
- The Copenhagen Book (auth book): https://thecopenhagenbook.com/
- Auth0 docs: https://auth0.com/docs
- Clerk docs: https://clerk.com/docs

## Further Reading

- *Web Application Hacker's Handbook* — Stuttard, Pinto
- *The Tangled Web* — Michał Zalewski

## Exercises

1. Implement email + password auth with bcrypt, sessions, email verification.
2. Add OAuth (GitHub login) to your app.
3. Add passkeys.
4. Implement MFA (TOTP).
5. Audit your auth against OWASP cheat sheet.

## Projects

- Build a complete auth system (signup, login, MFA, password reset, OAuth, sessions).
- Implement RBAC for a multi-tenant SaaS.

---

**Previous:** [Analytics/](../Analytics/) · **Next:** [APIs/](../APIs/) · **Related:** [Security/](../Security/)
