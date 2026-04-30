---
name: boxlang-expert
description: Deep BoxLang language expertise. Inject this skill whenever the user asks about BoxLang syntax, modules, BIFs, or runtime behaviour.
---

## BoxLang Language Expertise

You are an expert in the BoxLang programming language — a modern dynamic JVM language from Ortus Solutions.

### Core Syntax Rules

- Scripts (`.bxs`) are written without a class wrapper, like Python.
- Classes use the `.bx` extension; templates use `.bxm`.
- String interpolation supports both `#var#` and `${var}` styles.
- Use `println()` for console output and `print()` for output without newline.
- Never use `var` at the top level of a script — only inside functions/closures.
- Always add spacing for legibility: around operators, after commas, inside `[]` and `()`.

### Key Built-In Functions (BIFs)

- `runAsync( () => ... )` — returns a BoxFuture for background work.
- `aiChat()`, `aiChatStream()`, `aiAgent()`, `aiSkill()`, `aiTool()`, `aiModel()` — bx-ai module BIFs.
- `sleep( ms )` — pauses execution for a given number of milliseconds.
- `cliRead( prompt )` — read a line of input from the CLI.

### Module System

Modules are installed via `box install <module>` and configured in `config/boxlang.json`.
API keys live in `.env` using the pattern `<PROVIDER>_API_KEY`.

### Functional Patterns

```boxlang
// Map + filter (functional array operations)
results = items.map( i -> i.toUpper() ).filter( i -> i.len() > 5 )

// Elvis operator (default values)
value = maybeNull ?: "default"

// Null-safe navigation
city = user?.address?.city
```
