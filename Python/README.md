# Python

> Python for the web: Django, FastAPI, Flask. Plus tooling, packaging, testing.

---

## Purpose

Master Python for backend web development.

## Prerequisites

- Programming basics.

## Learning Outcome

You can build a Python web app, manage dependencies, test, and deploy.

## Dependencies

- Python 3.11+.

## Related Files

- [Django/](../Django/) · [FastAPI/](../FastAPI/) · [Backend/](../Backend/) · [Databases/](../Databases/)

## AI Instructions

When using Python:
1. Use Python 3.11+.
2. `uv` for package management (faster than pip + venv).
3. `ruff` for lint + format (replaces black + isort + flake8).
4. `mypy` or `pyright` for types.
5. `pytest` for tests.

## Human Notes

### Web frameworks
- **Django** — batteries-included. Best for content / CRUD apps.
- **FastAPI** — async, typed, fast. Best for APIs.
- **Flask** — minimal. Best for small apps.
- **Litestar** — modern alternative to FastAPI.

### Tooling
- **uv** — Astral's package manager. 10x faster than pip.
- **Ruff** — Astral's linter + formatter. Replaces many tools.
- **Pyright / Mypy** — type checkers.
- **pytest** — test framework.
- **pip-tools** — lock files for pip.

### Project structure
```
myapp/
  pyproject.toml
  src/myapp/
    __init__.py
    main.py
  tests/
```

### pyproject.toml (modern)
```toml
[project]
name = "myapp"
version = "0.1.0"
dependencies = ["fastapi", "uvicorn"]

[tool.ruff]
line-length = 100
target-version = "py311"

[tool.pytest.ini_options]
testpaths = ["tests"]
```

### Virtual environments
```bash
uv venv               # create
source .venv/bin/activate  # activate
uv pip install fastapi
```

Or use `uv run` to skip activation.

### Type hints
```python
def greet(name: str) -> str:
    return f"Hello, {name}"

from typing import Sequence
def first(items: Sequence[int]) -> int | None:
    return items[0] if items else None
```

### Async
```python
import asyncio

async def fetch_data():
    await asyncio.sleep(1)
    return {"data": 42}

asyncio.run(fetch_data())
```

### Common patterns
- Decorators (`@app.get("/")`).
- Context managers (`with open(...) as f:`).
- Generators (`def gen(): yield 1`).
- Dataclasses (`@dataclass class User: ...`).
- Pydantic models (FastAPI uses these for validation).

### Database
- SQLAlchemy (ORM).
- SQLModel (Pydantic + SQLAlchemy).
- asyncpg (async Postgres driver).
- Databases (async, by Encode).

### Testing
```python
def test_add():
    assert add(1, 2) == 3
```
Run: `pytest`

## Common Mistakes

- ❌ Using `pip` directly without venv.
- ❌ Not using types.
- ❌ Global state.
- ❌ Blocking I/O in async code.
- ❌ Mutable default args (`def f(x=[])`).

## Tools

- uv: https://github.com/astral-sh/uv
- Ruff: https://github.com/astral-sh/ruff
- Pyright: https://github.com/microsoft/pyright
- pytest: https://docs.pytest.org/

## References

- Python docs: https://docs.python.org/3/
- Real Python: https://realpython.com/
- Awesome Python: https://github.com/vinta/awesome-python

## Further Reading

- *Fluent Python* — Luciano Ramalho
- *Effective Python* — Brett Slatkin

## Exercises

1. Build a CLI tool with `click` or `typer`.
2. Build a FastAPI with type hints and async DB.

## Projects

- Build a Python backend with FastAPI + Postgres + JWT auth.

---

**Previous:** [NestJS/](../NestJS/) · **Next:** [Django/](../Django/) · **Related:** [FastAPI/](../FastAPI/)
