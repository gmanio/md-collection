# TypeScript review reference (PM skill)

Use with `typescript-pm-code-review/SKILL.md`. Same criteria as `typescript-code-review/reference.md`; read either file for deep checks.

## 1. Type system

- Assume **`strict`**-style settings; flag unsafe escapes.
- **`unknown` over `any`** for external data; narrow with guards or schema validation.
- **`as` / `!`**: sound narrowing only; flag runtime mismatch risk.
- **Generics**: constraints, variance, and API clarity.

## 2. Control flow and data

- **Narrowing** and edge cases (empty string, 0, NaN).
- **Exhaustiveness** on discriminated unions (`never` in default).

## 3. Async and errors

- **Promises**: missing `await`, wrong return types, error propagation.
- **Cancellation** where long-running work exists.

## 4. Module and API boundaries

- **Exports** and accidental surface area; breaking changes called out explicitly.
- **Runtime boundaries**: JSON, env, IPC vs types.

## 5. React (TSX)

- Hooks rules, dependency arrays, stale closures, unmount safety.

## 6. Security

- Injection, secrets in logs, authz at trust boundaries.

## 7. Performance (when relevant)

- Claim only with evidence.

## 8. Tests

- New behavior and regressions; mocks that match real behavior.
