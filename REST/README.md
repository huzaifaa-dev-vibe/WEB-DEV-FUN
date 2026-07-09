# REST

> Representational State Transfer. The default API style for the web.

---

## Purpose

Master REST API design: resources, methods, status codes, pagination, versioning.

## Prerequisites

- [APIs/](../APIs/), HTTP.

## Learning Outcome

You can design clean, idiomatic REST APIs.

## Dependencies

- HTTP.

## Related Files

- [APIs/](../APIs/) · [GraphQL/](../GraphQL/) · [REST/status-codes.md](status-codes.md) · [REST/examples.md](examples.md)

## AI Instructions

When designing REST:
1. Resource-oriented URLs: `/users`, `/users/123`, `/users/123/posts`.
2. Use HTTP methods correctly (GET/POST/PUT/PATCH/DELETE).
3. Use proper status codes. → [REST/status-codes.md](status-codes.md)
4. Cursor pagination for lists.
5. Version in URL (`/v1/`).
6. Consistent error format.
7. Validate all input.

## Human Notes

### Resources
- Plural nouns: `/users`, `/products`, `/orders`.
- Nest for relationships: `/users/123/orders`.
- Don't go deeper than 2 levels.

### HTTP methods
| Method | Use | Idempotent | Safe |
|---|---|---|---|
| GET | Read | Yes | Yes |
| POST | Create | No | No |
| PUT | Replace (full) | Yes | No |
| PATCH | Update (partial) | No | No |
| DELETE | Delete | Yes | No |

### Status codes
→ [REST/status-codes.md](status-codes.md)

Quick reference:
- 200 OK
- 201 Created
- 204 No Content
- 400 Bad Request
- 401 Unauthorized
- 403 Forbidden
- 404 Not Found
- 409 Conflict
- 422 Unprocessable Entity
- 429 Too Many Requests
- 500 Internal Server Error

### Examples
```http
# List
GET /v1/users?cursor=abc&limit=20

# Get one
GET /v1/users/123

# Create
POST /v1/users
Content-Type: application/json
{ "name": "Alice", "email": "a@b.com" }

# Update (full)
PUT /v1/users/123
{ "name": "Alice", "email": "a@b.com", "age": 30 }

# Update (partial)
PATCH /v1/users/123
{ "age": 31 }

# Delete
DELETE /v1/users/123

# Action (RPC-style, use sparingly)
POST /v1/users/123/activate
```

### Pagination
Cursor > offset:
```json
{
  "data": [...],
  "pagination": {
    "next_cursor": "eyJpZCI6MTIzfQ==",
    "has_more": true
  }
}
```

### Filtering
- `GET /products?category=electronics&min_price=100&max_price=500`
- Or: `GET /products?filter[category]=electronics`

### Sorting
- `GET /products?sort=-created_at,name`
- `-` prefix = descending.

### Field selection
- `GET /users?fields=id,name,email`
- Saves bandwidth.

### Embedding related
- `GET /users/123?include=orders,posts`

### Versioning
- URL: `/v1/`, `/v2/` (most common).
- Header: `Accept: application/vnd.api+json;version=1`.

### Error format
```json
{
  "error": {
    "code": "VALIDATION_ERROR",
    "message": "Email is required",
    "field": "email"
  }
}
```

### Idempotency
```http
POST /v1/payments
Idempotency-Key: 9c4f3b8a-1a2b-4c3d-8e5f-6a7b8c9d0e1f
```
Server stores key + response for 24h. Same key = same response.

### Rate limiting
- 1000 req/hour per user.
- 100 req/minute per IP.
- 429 with `Retry-After: 60`.

### HATEOAS (rarely used in practice)
Responses include links:
```json
{
  "data": { "id": 123 },
  "links": {
    "self": "/users/123",
    "orders": "/users/123/orders"
  }
}
```

## Common Mistakes

- ❌ Verbs in URL (`/getUser`).
- ❌ 200 for errors.
- ❌ Inconsistent naming.
- ❌ No pagination.
- ❌ No versioning.
- ❌ Exposing DB schema.
- ❌ Mixing singular and plural.

## Tools

- OpenAPI / Swagger.
- Postman / Insomnia / Bruno.

## References

- REST API Tutorial: https://restfulapi.net/
- Microsoft REST Guidelines: https://github.com/microsoft/api-guidelines
- Google API Design Guide: https://cloud.google.com/apis/design
- JSON:API spec: https://jsonapi.org/

## Exercises

1. Design a REST API for an e-commerce store.
2. Add cursor pagination.
3. Document with OpenAPI.

## Projects

- Build a REST API with auth, rate limiting, versioning.

---

**Previous:** [APIs/](../APIs/) · **Next:** [GraphQL/](../GraphQL/) · **Related:** [Backend/](../Backend/)
