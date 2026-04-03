---
name: typescript-pm-code-review
description: >-
  Reviews TypeScript changes for correctness, type safety, maintainability,
  security, and tests. Use when reviewing PRs, diffs, or .ts/.tsx files, or
  when the user asks for a TypeScript code review. Pairs with pm-code-reviewer
  agent; read reference.md for deep checks.
---

# TypeScript PM code review

## When this applies

- PR/diff review, pre-merge checks, or ad-hoc review of TS/TSX modules.
- Config touchpoints: `tsconfig*.json`, ESLint/Type-aware lint, build entrypoints.

## Workflow

1. **Scope**: Identify changed files, public API surface (exports), and runtime boundaries (I/O, auth, DB).
2. **Intent**: Infer the author’s goal from diff + messages; state it in one sentence if unclear, flag ambiguity.
3. **Types first**: `any`/`unknown` misuse, unsound assertions, incorrect generics, narrowing gaps, promise/async mistakes.
4. **Correctness**: Edge cases, error paths, race conditions, resource cleanup.
5. **Security**: Injection, SSRF, secrets, unsafe deserialization, authz gaps.
6. **Tests**: Coverage of new behavior and regressions; meaningful assertions (not only snapshots without reason).
7. **Consistency**: Naming, module boundaries, duplication vs shared utilities.

For expanded criteria and anti-patterns, read [reference.md](reference.md). For tone and comment shape, see [examples.md](examples.md).

## Severity labels

Use consistently:

| Label | Meaning |
|-------|---------|
| **Blocking** | Merge should wait: bugs, security, broken types/API contract, missing critical tests. |
| **Should fix** | Strongly recommended before or right after merge: maintainability, likely bugs, weak typing. |
| **Suggestion** | Improvement with clear benefit; optional before merge. |
| **Nit** | Style, micro-readability, preference; no merge block. |

## Output template

```markdown
## Summary
[One paragraph: what changed, risk level, recommendation merge/merge with fixes/hold]

## Blocking
- [file:line] ...

## Should fix
- ...

## Suggestions
- ...

## Nits
- ...

## Questions / assumptions
- ...
```

## TypeScript quick checks

- Prefer `unknown` over `any`; narrow before use.
- Avoid non-null assertion (`!`) unless invariant is documented in code or tests.
- `as` casts: justify; prefer type guards and discriminated unions.
- Async: no floating promises; handle rejections; correct `Promise` vs `async` return types.
- `strict` family: respect project `tsconfig`; do not widen types to silence errors without fixing root cause.

## Do not

- Bike-shed unrelated style if the repo already has formatter/linter.
- Request large refactors unrelated to the diff without strong justification.
- Label something Blocking without a concrete failure mode or policy violation.
