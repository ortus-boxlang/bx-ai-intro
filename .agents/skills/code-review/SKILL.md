---
name: code-review
description: BoxLang code review guidelines. Load this skill when asked to review, audit, or critique code for correctness, style, or best practices.
---

## Code Review Guidelines

When reviewing BoxLang code, check for the following in order of priority:

### 1. Correctness
- Variables at script scope must NOT use `var`; only use `var` inside functions.
- Verify null-safe navigation (`?.`) is used when properties may be absent.
- Confirm closures capture the right variables (closures capture by reference).

### 2. Style & Readability
- Operators and commas must have surrounding spaces: `a + b`, `fn( a, b )`.
- Use named arguments for clarity when calling BIFs: `aiChat( prompt: msg, params: { model: "..." } )`.
- Prefer lambdas (`->`) for simple one-liners and closures (`=>`) when outer scope is needed.

### 3. Performance
- Avoid repeated `aiChat()` calls inside loops — batch or pipeline where possible.
- Prefer `runAsync()` for work that can be non-blocking.

### 4. Response Format
Structure every code review as:

```
**Summary**: One-sentence verdict.

**Issues** (numbered list, most critical first):
1. ...

**Suggestions** (optional improvements):
- ...
```
