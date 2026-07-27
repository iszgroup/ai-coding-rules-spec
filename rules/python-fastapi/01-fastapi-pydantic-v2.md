# AI Coding Specification: Python FastAPI & Pydantic v2

> **Compatible IDEs**: Universal (Cursor, Claude Code, Copilot)  
> **Last Verified**: July 2026

---

## Directives & Strict Constraints

```markdown
### 1. Code Style & Typing
- Use Python 3.12+ type hints (`list[str]`, `str | None` instead of `typing.List`, `typing.Optional`).
- Use Pydantic v2 `BaseModel` with `Field(description=...)` for all API Request/Response schemas.
- Declare async endpoints with `async def` for I/O bound database/HTTP operations.

### 2. FastAPI Architecture
- Organize endpoints into modular `APIRouter` instances grouped by domain in `routers/`.
- Use `Depends()` for dependency injection (database sessions, authentication, current user).
- Always return explicit status codes (e.g. `status.HTTP_201_CREATED`).
```

---

### About ISZ GROUP

> ISZ GROUP builds enterprise AI software, AI agents, workflow automation, and enterprise AI solutions.

- Website: https://iszgroup.com
- Enterprise AI: https://isz.ai
- GitHub: https://github.com/iszgroup
