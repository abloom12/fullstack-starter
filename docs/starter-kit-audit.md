# Starter Kit Audit & TODOs

## Blocking bugs

- [ ] **Fix signup:** `apps/server/src/app.ts` passes `polarAccessToken: ''`, ignoring `POLAR_ACCESS_TOKEN`. Polar customer creation runs on signup, so it will fail with an empty token. Make Polar optional and pass/validate its real token, or remove it until billing is implemented.
- [ ] **Protect `/settings`:** the guard in `apps/web/src/routes/_app/route.tsx` is commented out, leaving `/settings` public.
- [ ] **Fix post-auth redirects:** login and signup redirect to `/forecast`, but that route no longer exists in source. The built route tree contains only `/`, `/login`, `/signup`, and `/settings`.
- [ ] **Wire Google login:** both social-auth button callbacks are no-ops despite server-side Google configuration.
- [ ] **Commit initial Drizzle migrations:** `packages/db/src/migrations` does not exist. A fresh database has no auth tables, so signup requires a manual `db:push`.
- [ ] **Fix environment examples:** `apps/server/.env.example` omits required `HOST`, and its example auth secret is shorter than the enforced 32-character minimum.
- [ ] **Update vulnerable dependencies:** `pnpm audit --prod` reported 37 issues, including 2 critical and 26 high. Update Better Auth/the adapter to a compatible patched version and update Vite.

## Priority todo list

### 1. Complete the minimal auth flow

- [ ] Implement email signup, login, logout, authenticated redirect, and redirect-back to the requested page.
- [ ] Render/use or remove the unused `rememberMe` field.
- [ ] Match signup client validation to the server's 12–128-character password policy.
- [ ] Redirect signed-in users away from `/login` and `/signup`.

### 2. Build the authenticated Settings page

- [ ] Show the current user and session.
- [ ] Support updating name and profile image.
- [ ] Support password changes, sign-out, and revoking other sessions.
- [ ] Add email verification and password-reset delivery before production use.
- [ ] Either implement 2FA, organization, admin, and Polar UI/tests, or remove those enabled plugins until needed.

### 3. Demonstrate the stack end-to-end

- [ ] Use `health.ping` and protected `health.me` from a small authenticated UI/example.
- [ ] Replace the placeholder `/` and `/settings` pages with a minimal landing page and app shell.
- [ ] Regenerate and commit `apps/web/src/routeTree.gen.ts`; it references deleted finance routes and is rewritten by Vite.

### 4. Add tests and CI

- [ ] Add Vitest/Fastify-inject tests for public/protected tRPC and auth behavior.
- [ ] Add Postgres integration tests: migration, signup, duplicate signup, login, session cookie, logout, and protected-route denial.
- [ ] Add Playwright coverage for signup → settings, login → intended redirect, Google initiation, and unauthenticated `/settings`.
- [ ] Add CI for install, format, lint, typecheck, tests, build, and dependency audit.

### 5. Make setup and deployment reproducible

- [ ] Document environment setup, Docker DB, migrations, development commands, and production migration policy in the root README.
- [ ] Change the Compose port mapping to `${DB_PORT}:5432`; the current `5432:${DB_PORT}` breaks when the host port changes.
- [ ] Add deployment/runtime configuration or Dockerfiles; Compose currently runs only Postgres.

## Broken quality gates observed

- `pnpm typecheck` — passes.
- `pnpm build` — passes.
- Server health endpoint and unauthenticated session endpoint — pass.
- `pnpm lint` — fails: the web ESLint config cannot resolve `tooling/eslint/react.ts`'s `./base` import, and `@acme/api` has five lint errors.
- `pnpm format` — fails: five files need formatting.
- There is no test runner, test suite, CI workflow, or deployment configuration.

## Focused preventative changes

- [ ] Make `getAuthErrorMessage` return its string instead of `{ en: string }`.
- [ ] Change `CurrencyField` from invalid `type="string"` to `type="text"` with `inputMode="decimal"`.
- [ ] Close the PostgreSQL pool during Fastify shutdown instead of relying on forced `process.exit`.
- [ ] Remove stale finance references, generic titles (`web`, `API`), and README claims for nonexistent `packages/ui` and `.vscode`.
