# Rust

> Rust: zero-cost abstractions, memory safety without GC. The future of systems code.

---

## Purpose

Build fast, safe backend services with Rust (Axum, Actix).

## Prerequisites

- Programming experience. Rust has a learning curve.

## Learning Outcome

You can build a Rust web service, manage ownership/borrowing, and ship a binary.

## Dependencies

- Rust (rustup).

## Related Files

- [Backend/](../Backend/) · [Go/](../Go/) · [System-Design/](../System-Design/)

## AI Instructions

When using Rust:
1. Use Axum (modern) or Actix (mature).
2. Use Tokio for async runtime.
3. Use `sqlx` (compile-time checked SQL) or `diesel`.
4. Use `serde` for JSON.
5. Use `clippy` for linting.
6. Use `cargo` for everything.
7. Don't fight the borrow checker. Restructure.

## Human Notes

### Install
```bash
curl --proto '=https' --tlsv1.2 -sSf https://sh.rustup.rs | sh
```

### Hello Axum
```rust
use axum::{routing::get, Router, Json};
use serde::Serialize;

#[derive(Serialize)]
struct User { id: u32, name: String }

async fn users() -> Json<Vec<User>> {
    Json(vec![User { id: 1, name: "Alice".into() }])
}

#[tokio::main]
async fn main() {
    let app = Router::new().route("/users", get(users));
    let listener = tokio::net::TcpListener::bind("0.0.0.0:8080").await.unwrap();
    axum::serve(listener, app).await.unwrap();
}
```

### Ownership / borrowing
```rust
fn main() {
    let s = String::from("hello");
    takes_ownership(s);          // s moved
    // s no longer valid here

    let n = 5;
    makes_copy(n);               // i32 is Copy
    println!("{}", n);           // still valid

    let s2 = String::from("hi");
    borrows(&s2);                // borrowed
    println!("{}", s2);          // still valid
}

fn takes_ownership(s: String) {}
fn makes_copy(n: i32) {}
fn borrows(s: &String) {}
```

### Structs + traits
```rust
trait Greet {
    fn greet(&self) -> String;
}

struct User { name: String }

impl Greet for User {
    fn greet(&self) -> String {
        format!("Hello, {}!", self.name)
    }
}
```

### Error handling
```rust
use thiserror::Error;

#[derive(Error, Debug)]
enum AppError {
    #[error("not found")]
    NotFound,
    #[error("db error: {0}")]
    Db(#[from] sqlx::Error),
}

type Result<T> = std::result::Result<T, AppError>;
```

### Async (Tokio)
```rust
#[tokio::main]
async fn main() {
    let result = async_fn().await;
}

async fn async_fn() -> u32 { 42 }
```

### Database (sqlx)
```rust
use sqlx::postgres::PgPool;

let pool = PgPool::connect("postgres://...").await?;

let user: User = sqlx::query_as::<_, User>("SELECT * FROM users WHERE id = $1")
    .bind(1)
    .fetch_one(&pool)
    .await?;
```

### Testing
```rust
#[cfg(test)]
mod tests {
    #[test]
    fn it_works() {
        assert_eq!(2 + 2, 4);
    }
}
```
Run: `cargo test`

### Cargo
```bash
cargo new myapp
cargo build
cargo run
cargo test
cargo clippy
cargo fmt
cargo build --release  # optimized
```

### Performance
- No GC. Predictable latency.
- Compiles to native binary.
- Often faster than Go, sometimes matches C.
- Tiny memory footprint.

### When to use Rust
- Performance-critical.
- Low-latency services.
- CLI tools.
- WASM.
- Systems code.

### When NOT to use
- Rapid prototyping (use Python/Node).
- Simple CRUD (use anything else).
- Small team that doesn't know Rust.

## Common Mistakes

- ❌ Fighting the borrow checker.
- ❌ `unwrap()` everywhere (panic risk).
- ❌ Not using `thiserror` / `anyhow`.
- ❌ Sync code in async context.
- ❌ Premature optimization.

## Tools

- Rust docs: https://doc.rust-lang.org/
- Rust by Example: https://doc.rust-lang.org/rust-by-example/
- clippy: linter (built into cargo)
- rust-analyzer: LSP
- The Rust Book: https://doc.rust-lang.org/book/

## Further Reading

- *The Rust Programming Language* — Steve Klabnik & Carol Nichols (free)
- *Programming Rust* — Jim Blandy & Jason Orendorff
- *Zero to Production in Rust* — Luca Palmieri

## Exercises

1. Build a CLI tool.
2. Build an HTTP API with Axum.
3. Add a Postgres connection with sqlx.

## Projects

- Build a URL shortener in Rust.
- Build a WebSocket server.

---

**Previous:** [Go/](../Go/) · **Next:** [Java/](../Java/) · **Related:** [Backend/](../Backend/)
