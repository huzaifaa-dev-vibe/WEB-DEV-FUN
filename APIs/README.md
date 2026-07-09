# APIs

> The contract between systems. Design them well or pay forever.

---

## Purpose

Design APIs that are consistent, predictable, versioned, and forgiving.

## Prerequisites

- [Backend/](../Backend/) basics, HTTP.

## Learning Outcome

You can design a REST or GraphQL API that developers love to use.

## Dependencies

- Backend framework.

## Related Files

- [REST/](../REST/) · [GraphQL/](../GraphQL/) · [APIs/idempotency.md](idempotency.md) · [APIs/versioning.md](versioning.md) · [APIs/errors.md](errors.md) · [APIs/rate-limiting.md](rate-limiting.md)

## AI Instructions

When designing APIs:
1. **REST for CRUD**, GraphQL for complex queries.
2. **Use proper status codes.** → [REST/status-codes.md](../REST/status-codes.md)
3. **Idempotency keys** for mutations. → [APIs/idempotency.md](idempotency.md)
4. **Version from day 1.** → [APIs/versioning.md](versioning.md)
5. **Consistent error format.** → [APIs/errors.md](errors.md)
6. **Validate all input** (Zod).
7. **Rate limit** public endpoints.
8. **Document** with OpenAPI.
9. **Pagination** for lists (cursor > offset).
10. **Don't expose DB schema.** DTOs.

## Human Notes

### REST vs GraphQL

| | REST | GraphQL |
|---|---|---|
| Shape | Fixed endpoints | Single endpoint, query shape |
| Over-fetching | Common | Solved |
| Under-fetching | Common | Solved |
| Caching | HTTP cache (easy) | Harder (custom) |
| Versioning | URL path (/v1/) | Schema evolution |
| Tooling | Mature | Good |
| Learning curve | Lower | Higher |
| File uploads | Easy | Awkward |
| Public API | Yes | Less common |

Default: **REST** for public APIs and CRUD. GraphQL for complex client needs (e.g., mobile app, complex dashboards).

### REST principles
- Resource-oriented: `/users`, `/users/123`, `/users/123/posts`.
- HTTP methods: GET (read), POST (create), PUT (replace), PATCH (update), DELETE.
- Stateless (each request has everything needed).
- Cacheable (use Cache-Control).
- Layered (client doesn't know about intermediaries).

→ [REST/](../REST/)

### Status codes
- 2xx success.
- 3xx redirect.
- 4xx client error.
- 5xx server error.

→ [REST/status-codes.md](../REST/status-codes.md)

Common:
- 200 OK
- 201 Created
- 204 No Content
- 400 Bad Request (validation)
- 401 Unauthorized (not logged in)
- 403 Forbidden (logged in, can't do)
- 404 Not Found
- 409 Conflict (duplicate)
- 422 Unprocessable Entity
- 429 Too Many Requests
- 500 Internal Server Error
- 502 Bad Gateway
- 503 Service Unavailable
- 504 Gateway Timeout

### Idempotency
- GET, PUT, DELETE — idempotent by HTTP spec.
- POST — not idempotent (use Idempotency-Key header for retries).

→ [APIs/idempotency.md](idempotency.md)

### Versioning
- URL: `/v1/users` (most common, simple).
- Header: `Accept: application/vnd.api+json;version=1` (cleaner, harder).
- Query: `?version=1` (avoid).

→ [APIs/versioning.md](versioning.md)

### Errors
Consistent format:
```json
{
  "error": {
    "code": "VALIDATION_ERROR",
    "message": "Email is required",
    "field": "email",
    "details": { /* optional */ }
  }
}
```
→ [APIs/errors.md](errors.md)

### Pagination
- **Offset/limit** — simple, slow for large offsets.
- **Cursor** — fast, stable, harder to implement. Prefer.
- **Page** — UI-friendly, slow at scale.

```json
{
  "data": [...],
  "pagination": {
    "next_cursor": "abc123",
    "has_more": true
  }
}
```

### Filtering & sorting
- `GET /products?filter[category]=electronics&sort=-created_at`
- Or: `GET /products?category=electronics&sort=-created_at`
- Be consistent.

### Rate limiting
- Per IP + per user.
- Tiered (anonymous, authenticated, premium).
- 429 with `Retry-After` header.
- → [APIs/rate-limiting.md](rate-limiting.md)

### Authentication
- Bearer token in `Authorization` header.
- API key in header.
- OAuth 2.0.
- mTLS (high-security).

### CORS
- Allowlist origins, not `*`.
- → [Security/cors.md](../Security/cors.md)

### Documentation
- OpenAPI (Swagger) — REST.
- GraphQL schema — built-in docs.
- Provide examples for every endpoint.
- Try-it-now (Swagger UI, Redoc, Stoplight).

### Testing
- Unit tests for handlers.
- Integration tests for the full request/response.
- Contract tests (Pact) for cross-service.
- Load tests (k6).
- E2E for critical paths.

## Common Mistakes

- ❌ 200 OK for errors.
- ❌ Inconsistent error format.
- ❌ No pagination.
- ❌ No rate limiting.
- ❌ Exposing DB schema.
- ❌ No versioning.
- ❌ No idempotency for retries.
- ❌ No documentation.
- ❌ Verb in URL (`/getUser` instead of `GET /users/123`).
- ❌ Inconsistent naming (camelCase vs snake_case mix).
- ❌ Trusting client input.
- ❌ No CORS allowlist.

## Tools

- OpenAPI: https://www.openapis.org/
- Swagger UI: https://swagger.io/tools/swagger-ui/
- Redoc: https://redocly.com/redoc
- Stoplight: https://stoplight.io/
- Postman: https://www.postman.com/
- Insomnia: https://insomnia.rest/
- Bruno: https://www.usebruno.com/ (open-source)
- Hoppscotch: https://hoppscotch.io/

## References

- REST API Tutorial: https://restfulapi.net/
- HTTP Spec: https://www.rfc-editor.org/rfc/rfc9110
- GraphQL: https://graphql.org/
- Microsoft REST API Guidelines: https://github.com/microsoft/api-guidelines
- Google API Design Guide: https://cloud.google.com/apis/design

## Further Reading

- *Designing Web APIs* — Brenda Jin et al.
- *API Design Patterns* — JJ Geewax
- *The Tangled Web* — Michał Zalewski

## Exercises

1. Design a REST API for a blog (posts, comments, users).
2. Add idempotency keys to a payment endpoint.
3. Document your API with OpenAPI.

## Projects

- Build a public REST API with rate limiting, auth, versioning, and OpenAPI docs.
- Build a GraphQL API with subscriptions.

---

**Previous:** [Authentication/](../Authentication/) · **Next:** [REST/](../REST/) · **Related:** [GraphQL/](../GraphQL/)
