---
name: security
description: Security review for BoxLang and web applications. Load this skill when asked to review code for vulnerabilities, injection risks, or insecure patterns.
---

## Security Review Guidelines

When performing a security review of BoxLang code or application design, check for the following threats:

### Input Validation
- All user-supplied input must be validated or sanitised before use.
- Never pass raw user input as a prompt to an AI model without stripping injection phrases.
- Use allowlists over denylists for input validation.

### Secrets & Credentials
- API keys and secrets must live in `.env`, never hard-coded.
- Never log raw request/response bodies when they may contain credentials (`logResponseToConsole: false`).

### Injection
- **Prompt Injection**: Treat AI responses as untrusted data — do not execute strings returned by an AI directly.
- **SQL Injection**: Always use parameterised queries, never string concatenation.
- **Path Traversal**: Canonicalise file paths and reject paths containing `..`.

### Output Encoding
- Escape all user-generated content before rendering in HTML contexts.
- Set `Content-Security-Policy` headers on any web endpoints.

### Response Format
Structure every security review as:

```
**Risk Level**: Critical / High / Medium / Low / Info

**Findings** (numbered, most critical first):
1. [RISK] Description — Remediation

**Clean Bill of Health** (if no issues found):
No security issues detected.
```
