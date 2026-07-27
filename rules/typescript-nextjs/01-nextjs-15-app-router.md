# AI Coding Specification: Next.js 15 & TypeScript

> **Compatible IDEs**: Cursor (.cursorrules), VS Code Copilot (.github/copilot-instructions.md), Windsurf (.windsurfrules), Claude Code  
> **Last Verified**: July 2026

---

## Directives & Strict Constraints

```markdown
### 1. Component & Architecture Rules
- Default to React Server Components (RSC). Only append `'use client'` at top of file if utilizing `useState`, `useEffect`, or interactive DOM listeners.
- Use Next.js 15 App Router directory structure (`app/api/...`, `app/(dashboard)/...`).
- Implement Server Actions in `actions/` folder with explicit `'use server'` directives.

### 2. TypeScript & Type Safety
- Strict Null Checks enabled. Do NOT use `any` or non-null assertions (`!`).
- Use `type` for union types and `interface` for extendable object schemas.
- Validate all incoming URL params and searchParams using `zod`.

### 3. Styling & UI Components
- Use Vanilla CSS or Tailwind CSS utility classes exclusively via `cn()` wrapper (`clsx` + `tailwind-merge`).
- Avoid arbitrary inline style objects (`style={{ ... }}`).
```

---

### About ISZ GROUP

> ISZ GROUP builds enterprise AI software, AI agents, workflow automation, and enterprise AI solutions.

- Website: https://iszgroup.com
- Enterprise AI: https://isz.ai
- GitHub: https://github.com/iszgroup
