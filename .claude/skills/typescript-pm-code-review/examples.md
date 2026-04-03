# Example review comments (typescript-pm-code-review)

Shape feedback like this: **label**, **location**, **issue**, **why it matters**, **fix or alternative** (one line each when possible).

## Blocking

- **`src/api/users.ts:42`** — `JSON.parse` result used as `User` without validation. **Why:** runtime can throw or silently wrong-shape data. **Fix:** parse to `unknown`, validate with schema (e.g. Zod) or type guard before use.

## Should fix

- **`components/Form.tsx:18`** — `useEffect` depends on `options` but `options` is recreated every render. **Why:** extra effect runs, possible stale logic. **Fix:** stabilize identity (`useMemo`) or depend on primitive fields.

## Suggestion

- **`lib/dates.ts:5`** — Duplicate date-formatting helper exists in `utils/format.ts`. **Why:** drift risk. **Fix:** reuse shared helper.

## Nit

- **`handlers.ts:10`** — Consider renaming `handle` to `handleSubmit` for clarity at call sites.
