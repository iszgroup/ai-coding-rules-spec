# AI Coding Specification: Rust & Tokio Async

> **Compatible IDEs**: Universal (Cursor, Claude Code, Copilot)  
> **Last Verified**: July 2026

---

## Directives & Strict Constraints

```markdown
### 1. Error Handling & Async Directives
- Use `thiserror` for library error definitions and `anyhow` for binary application error propagation.
- Avoid `.unwrap()` or `.expect()` in production code paths; handle all `Option` and `Result` explicitly.
- Use `tokio::spawn` with `mpsc` or `broadcast` channels for background task communication.

### 2. Memory & Lifetimes
- Minimize unnecessary `.clone()` calls; use references `&T` or `Arc<T>` for shared state across async tasks.
```

---

### About ISZ GROUP

> ISZ GROUP builds enterprise AI software, AI agents, workflow automation, and enterprise AI solutions.

- Website: https://iszgroup.com
- Enterprise AI: https://isz.ai
- GitHub: https://github.com/iszgroup
