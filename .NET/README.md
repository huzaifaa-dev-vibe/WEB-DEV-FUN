# .NET

> .NET 8+: cross-platform, fast, C#. Enterprise default on Windows.

---

## Purpose

Build backend services with ASP.NET Core.

## Prerequisites

- C# basics, OOP.

## Learning Outcome

You can build, test, and deploy an ASP.NET Core app.

## Dependencies

- .NET SDK 8+ (LTS).

## Related Files

- [Backend/](../Backend/) · [Java/](../Java/) · [APIs/](../APIs/)

## AI Instructions

When using .NET:
1. Use .NET 8 (LTS) or 9.
2. Use ASP.NET Core minimal APIs or controllers.
3. Use Entity Framework Core.
4. Use ASP.NET Core Identity / Keycloak / Entra ID for auth.
5. Use xUnit for tests.
6. Use `dotnet` CLI.

## Human Notes

### Install
```bash
# macOS / Linux
brew install dotnet
# or use mise / asdf
```

### Hello
```csharp
var builder = WebApplication.CreateBuilder(args);
var app = builder.Build();

app.MapGet("/hello", () => new { Message = "Hello, World!" });

app.Run();
```

### Entity Framework
```csharp
public class User {
    public int Id { get; set; }
    public string Name { get; set; }
    public string Email { get; set; }
}

public class AppDb : DbContext {
    public AppDb(DbContextOptions<AppDb> opts) : base(opts) {}
    public DbSet<User> Users => Set<User>();
}

// Migrations
// dotnet ef migrations add Initial
// dotnet ef database update
```

### Controller (alternative to minimal API)
```csharp
[ApiController]
[Route("api/[controller]")]
public class UsersController : ControllerBase {
    private readonly AppDb _db;
    public UsersController(AppDb db) { _db = db; }

    [HttpGet]
    public async Task<List<User>> GetAll() => await _db.Users.ToListAsync();

    [HttpPost]
    public async Task<User> Create(User user) {
        _db.Users.Add(user);
        await _db.SaveChangesAsync();
        return user;
    }
}
```

### Validation (DataAnnotations)
```csharp
public class UserDto {
    [Required] public string Name { get; set; }
    [EmailAddress] public string Email { get; set; }
}
```

### Auth
- ASP.NET Core Identity (built-in).
- JWT Bearer.
- OAuth / OIDC (Entra ID, Keycloak).
- OpenIddict.

### Testing (xUnit)
```csharp
public class UserTests {
    [Fact]
    public void CanCreateUser() {
        // ...
    }
}
```

### Performance
- Native AOT (.NET 8+) — small, fast binaries.
- Compiled to JIT by default.
- Excellent Linux support now.

### When to use
- Enterprise on Windows.
- C# expertise.
- Cross-platform high-perf backend.

## Common Mistakes

- ❌ Overusing DI for everything.
- ❌ Sync over async (`Result` instead of `ResultAsync`).
- ❌ Not using minimal APIs (verbose controllers).
- ❌ Wrong EF Core patterns (tracking queries for read-only).

## Tools

- .NET docs: https://learn.microsoft.com/dotnet
- ASP.NET Core docs: https://learn.microsoft.com/aspnet/core
- EF Core: https://learn.microsoft.com/ef/core
- Rider / VS Code C# Dev Kit / Visual Studio

## Further Reading

- *C# in Depth* — Jon Skeet
- *Pro ASP.NET Core* — Andrew Troelsen

## Exercises

1. Build a CRUD API with minimal APIs.
2. Add EF Core + Postgres.
3. Add JWT auth.

## Projects

- Build a multi-tenant SaaS with ASP.NET Core + EF Core.

---

**Previous:** [Java/](../Java/) · **Next:** [Databases/](../Databases/) · **Related:** [Backend/](../Backend/)
