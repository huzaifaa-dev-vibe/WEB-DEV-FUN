# Go

> Go: simple, fast, concurrent. Born at Google. Great for backends.

---

## Purpose

Build high-performance, concurrent backend services with Go.

## Prerequisites

- Programming basics.

## Learning Outcome

You can build, deploy, and scale a Go backend.

## Dependencies

- Go 1.22+.

## Related Files

- [Backend/](../Backend/) · [APIs/](../APIs/) · [Docker/](../Docker/) · [Microservices/](../Microservices/)

## AI Instructions

When using Go:
1. Use Go 1.22+.
2. Use `net/http` (stdlib) or a router (Gin, Echo, Chi, Fiber).
3. Use `context` for cancellation/timeouts.
4. Use goroutines + channels for concurrency.
5. Use `golangci-lint` for linting.
6. Use `pprof` for profiling.
7. Single static binary — easy deploy.

## Human Notes

### Hello HTTP
```go
package main

import (
    "encoding/json"
    "net/http"
)

type User struct {
    ID   int    `json:"id"`
    Name string `json:"name"`
}

func usersHandler(w http.ResponseWriter, r *http.Request) {
    users := []User{{ID: 1, Name: "Alice"}}
    w.Header().Set("Content-Type", "application/json")
    json.NewEncoder(w).Encode(users)
}

func main() {
    http.HandleFunc("/users", usersHandler)
    http.ListenAndServe(":8080", nil)
}
```

### Goroutines + channels
```go
func worker(id int, jobs <-chan int, results chan<- int) {
    for j := range jobs {
        results <- j * 2
    }
}

func main() {
    jobs := make(chan int, 100)
    results := make(chan int, 100)
    for w := 1; w <= 3; w++ {
        go worker(w, jobs, results)
    }
    for j := 1; j <= 5; j++ {
        jobs <- j
    }
    close(jobs)
    for r := 1; r <= 5; r++ {
        fmt.Println(<-results)
    }
}
```

### Context
```go
ctx, cancel := context.WithTimeout(context.Background(), 5*time.Second)
defer cancel()

req, _ := http.NewRequestWithContext(ctx, "GET", url, nil)
res, err := http.DefaultClient.Do(req)
```

### Errors
```go
if err != nil {
    return fmt.Errorf("doing X: %w", err)
}

// Go 1.13+ wrapping
errors.Is(err, sql.ErrNoRows)
var pathErr *fs.PathError
errors.As(err, &pathErr)
```

### Structs + interfaces
```go
type UserStore interface {
    Get(id int) (*User, error)
}

type PostgresStore struct { db *sql.DB }

func (s *PostgresStore) Get(id int) (*User, error) {
    // ...
}
```

### Testing
```go
func TestAdd(t *testing.T) {
    if add(1, 2) != 3 {
        t.Error("expected 3")
    }
}
```
Run: `go test ./...`

### Modules
```bash
go mod init myapp
go get github.com/gin-gonic/gin
```

### Project structure
Standard: https://github.com/golang-standards/project-layout

### Performance
- Built-in profiler (`net/http/pprof`).
- Compiled to single binary.
- Tiny memory footprint.
- Fast startup (great for serverless).

### Frameworks
- **Stdlib only** — often enough.
- **Gin** — Express-like.
- **Echo** — minimal, fast.
- **Chi** — idiomatic, lightweight.
- **Fiber** — Express-like, fast (Fasthttp).
- **Huma** (modern, OpenAPI-first).

### Go vs other backends
- Faster than Node/Python/Ruby.
- Slower than Rust.
- Simpler than Rust, Java.
- Great for microservices, CLIs, network services.

## Common Mistakes

- ❌ Not using `context`.
- ❌ Goroutine leaks (no cancellation).
- ❌ Not handling errors (Go forces you to; don't ignore).
- ❌ Sync primitives misuse (race conditions).
- ❌ Global state.

## Tools

- Go docs: https://go.dev/doc/
- Go by Example: https://gobyexample.com/
- golangci-lint: https://golangci-lint.run/
- pprof: https://pkg.go.dev/net/http/pprof
- Delve: debugger

## Further Reading

- *The Go Programming Language* — Donovan & Kernighan
- *100 Go Mistakes and How to Avoid Them* — Teiva Harsanyi

## Exercises

1. Build an HTTP API with stdlib.
2. Add goroutines for parallel work.
3. Add graceful shutdown.

## Projects

- Build a high-throughput URL shortener in Go.
- Build a TCP chat server.

---

**Previous:** [Ruby/](../Ruby/) · **Next:** [Rust/](../Rust/) · **Related:** [Backend/](../Backend/)
