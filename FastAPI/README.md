# FastAPI

> Modern, fast, async Python web framework. Type hints native. Built on Starlette + Pydantic.

---

## Purpose

Build async, typed, fast APIs with FastAPI.

## Prerequisites

- [Python/](../Python/), async basics.

## Learning Outcome

You can build a FastAPI app with async endpoints, Pydantic validation, and OpenAPI docs.

## Dependencies

- Python 3.11+.

## Related Files

- [Python/](../Python/) · [Django/](../Django/) · [Backend/](../Backend/) · [APIs/](../APIs/)

## AI Instructions

When using FastAPI:
1. Use async endpoints (`async def`).
2. Use Pydantic for input/output schemas.
3. Use dependency injection for DB, auth.
4. Auto OpenAPI at `/docs`.
5. Use `uvicorn` or `hypercorn` ASGI server.

## Human Notes

### Why FastAPI
- Type hints → auto validation + docs.
- Async native.
- Fast (Starlette + Pydantic core).
- Auto OpenAPI docs.
- Modern Python.

### Basic app
```python
from fastapi import FastAPI, Depends, HTTPException
from pydantic import BaseModel, EmailStr
from sqlalchemy.ext.asyncio import AsyncSession

app = FastAPI()

class UserCreate(BaseModel):
    name: str
    email: EmailStr
    age: int | None = None

class UserOut(BaseModel):
    id: int
    name: str
    email: str

@app.post('/users', response_model=UserOut)
async def create_user(user: UserCreate, db: AsyncSession = Depends(get_db)):
    db_user = await db_user_create(db, user)
    return db_user

@app.get('/users/{user_id}', response_model=UserOut)
async def get_user(user_id: int, db: AsyncSession = Depends(get_db)):
    user = await db_user_get(db, user_id)
    if not user:
        raise HTTPException(404, 'User not found')
    return user
```

### Dependency injection
```python
async def get_db():
    async with SessionLocal() as session:
        yield session

async def get_current_user(token: str = Depends(oauth2_scheme), db = Depends(get_db)):
    user = verify_token(token)
    if not user:
        raise HTTPException(401)
    return user

@app.get('/me')
async def me(user = Depends(get_current_user)):
    return user
```

### Pydantic
```python
from pydantic import BaseModel, Field, EmailStr

class CreateUser(BaseModel):
    name: str = Field(min_length=1, max_length=100)
    email: EmailStr
    age: int = Field(ge=13, le=150)
    tags: list[str] = []
```

### Async DB
- SQLAlchemy 2.0 async.
- asyncpg (Postgres).
- SQLModel (Pydantic + SQLAlchemy).

### Background tasks
```python
from fastapi import BackgroundTasks

@app.post('/send-email')
async def send_email(background_tasks: BackgroundTasks):
    background_tasks.add_task(do_send_email, 'a@b.com')
    return {'status': 'queued'}
```

For heavier: Celery, Arq, Dramatiq.

### WebSockets
```python
from fastapi import WebSocket

@app.websocket('/ws')
async def ws(websocket: WebSocket):
    await websocket.accept()
    while True:
        data = await websocket.receive_text()
        await websocket.send_text(f'Echo: {data}')
```

### OpenAPI
- Auto docs at `/docs` (Swagger).
- ReDoc at `/redoc`.
- Schema at `/openapi.json`.

### Testing
```python
from fastapi.testclient import TestClient

client = TestClient(app)

def test_create_user():
    res = client.post('/users', json={'name': 'A', 'email': 'a@b.com'})
    assert res.status_code == 201
```

### Project structure
```
app/
  main.py
  deps.py
  models/
  schemas/
  routers/
  services/
  db.py
tests/
```

### Performance
- Run with `uvicorn app.main:app --workers 4`.
- Use `gunicorn -k uvicorn.workers.UvicornWorker` for prod.
- Pydantic v2 (much faster than v1).

## Common Mistakes

- ❌ Blocking I/O in async endpoints.
- ❌ Not using async DB drivers.
- ❌ Overusing `Depends` (can hurt perf).
- ❌ Not validating input (Pydantic is your friend).

## Tools

- FastAPI docs: https://fastapi.tiangolo.com/
- Uvicorn: https://www.uvicorn.org/
- Pydantic: https://docs.pydantic.dev/
- SQLModel: https://sqlmodel.tiangolo.com/

## References

- FastAPI: https://fastapi.tiangolo.com/

## Further Reading

- *Building Data Science Applications with FastAPI* — Francois Dion

## Exercises

1. Build a CRUD API with async DB.
2. Add JWT auth.
3. Add background tasks.

## Projects

- Build a real-time chat with FastAPI + WebSockets + Postgres.

---

**Previous:** [Django/](../Django/) · **Next:** [PHP/](../PHP/) · **Related:** [Python/](../Python/)
