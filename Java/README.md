# Java

> Java + Spring Boot: the enterprise default. JVM performance, huge ecosystem.

---

## Purpose

Build enterprise backend services with Java + Spring Boot.

## Prerequisites

- Programming basics, OOP.

## Learning Outcome

You can build, test, and deploy a Spring Boot app.

## Dependencies

- JDK 21+ (LTS).

## Related Files

- [Backend/](../Backend/) · [.NET/](../.NET/) · [APIs/](../APIs/)

## AI Instructions

When using Java:
1. Use JDK 21+ (LTS).
2. Use Spring Boot 3+.
3. Use Spring Data JPA / Hibernate.
4. Use Spring Security for auth.
5. Use Maven or Gradle.
6. Use JUnit 5 + Mockito for tests.
7. Use Spring Profiles for env-specific config.

## Human Notes

### Spring Boot
The de-facto Java web framework.

```bash
# Spring Initializr: https://start.spring.io/
# Or:
curl https://start.spring.io/starter.zip -d dependencies=web,jpa,postgresql -o myapp.zip
```

### Hello
```java
@RestController
@SpringBootApplication
public class App {
    public static void main(String[] args) {
        SpringApplication.run(App.class, args);
    }

    @GetMapping("/hello")
    public String hello() {
        return "Hello, World!";
    }
}
```

### Entity
```java
@Entity
public class User {
    @Id @GeneratedValue
    private Long id;
    private String name;
    private String email;
    // getters, setters
}

public interface UserRepository extends JpaRepository<User, Long> {
    Optional<User> findByEmail(String email);
}
```

### Controller
```java
@RestController
@RequestMapping("/users")
public class UserController {
    @Autowired private UserRepository repo;

    @GetMapping
    public List<User> list() { return repo.findAll(); }

    @PostMapping
    public User create(@Valid @RequestBody UserDto dto) {
        User u = new User();
        u.setName(dto.getName());
        u.setEmail(dto.getEmail());
        return repo.save(u);
    }
}
```

### Validation
```java
public class UserDto {
    @NotBlank private String name;
    @Email private String email;
}
```

### Auth (Spring Security)
- OAuth2 / OIDC.
- JWT.
- Sessions.

### Profiles + Config
```yaml
# application.yml
spring:
  profiles:
    active: ${SPRING_PROFILES_ACTIVE:dev}
  datasource:
    url: ${DATABASE_URL}
```

### Testing (JUnit 5)
```java
@SpringBootTest
class UserTests {
    @Test
    void createUser() {
        // ...
    }
}
```

### Performance
- JVM: JIT, GC tuning.
- Spring Boot 3+: GraalVM native images.
- Virtual threads (Java 21+): massive concurrency.
- Connection pooling (HikariCP).

### When to use
- Enterprise.
- Big team.
- JVM ecosystem.
- Existing Java code.

### When NOT
- Startup (use Node/Python for speed).
- Small APIs.

## Common Mistakes

- ❌ Over-abstraction (AbstractFactoryManager beans).
- ❌ Anemic domain model.
- ❌ Sync I/O blocking.
- ❌ Wrong GC for workload.
- ❌ Not using Spring Profiles.

## Tools

- Spring Initializr: https://start.spring.io/
- Spring docs: https://docs.spring.io/spring-boot/docs/current/reference/html/
- IntelliJ IDEA: best Java IDE.

## Further Reading

- *Spring in Action* — Craig Walls
- *Effective Java* — Joshua Bloch

## Exercises

1. Build a CRUD API with Spring Boot.
2. Add Spring Security with JWT.
3. Add tests with JUnit 5.

## Projects

- Build a microservice with Spring Boot + Postgres + Redis.

---

**Previous:** [Rust/](../Rust/) · **Next:** [.NET/](../.NET/) · **Related:** [Backend/](../Backend/)
