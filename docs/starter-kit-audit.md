# Starter Kit Audit & TODOs

This audit reflects the current source tree and the quality checks run locally.

## Release blockers

- [ ] **Commit an initial Drizzle migration.** `packages/db/src/migrations/` exists but is empty. A fresh database has no auth tables, so the documented `pnpm db:migrate` bootstrap cannot create them. Generate, review, commit, and apply the initial migration before relying on signup or deploying.
- [ ] **Fix the server environment example.** `HOST` is required by `apps/server/src/env.ts` but absent from `apps/server/.env.example`; its example `BETTER_AUTH_SECRET` is also shorter than the enforced 32-character minimum. Copying the example therefore prevents the server from starting.
- [ ] **Upgrade vulnerable dependencies.** `pnpm audit --prod` reports 37 vulnerabilities: 2 critical, 26 high, 6 moderate, and 3 low. In particular, the locked Better Auth `1.6.8` is vulnerable (the audit identifies `>=1.6.22` as patched), and Vite `8.0.9` is below the audit's patched `8.0.16`. Update direct packages and compatible transitive dependencies, then rerun the audit and the full auth flow.
- [ ] **Do not show a nonfunctional Google control.** Google configuration is now optional and the provider is registered only when both server credentials are set. However, both visible Google buttons still use `onClick={() => {}}`. Hide/remove them until `authClient.signIn.social({ provider: 'google' })` is wired and the Google OAuth callback is configured.
- [ ] **Decide on the enabled Better Auth features before production.** `admin`, `organization`, and `twoFactor` plugins expose server functionality, but there is no corresponding product UI or test coverage. Implement and test them, or remove the plugins. Email verification and password-reset delivery are also intentionally unconfigured; do not require verified email until delivery is implemented.

## Auth and application flow

- [x] Email/password signup, sign-in, sign-out, session-aware home, and redirect-back to `/settings` are implemented.
- [x] `/settings` is protected by a route-level session check.
- [x] Client password validation matches the configured 12–128-character server policy.
- [x] The auth server validates its environment, uses explicit CORS origins with credentials, rate limiting, Helmet, and Better Auth trusted origins.
- [ ] Add account/session management if needed: list and revoke other sessions, account deletion, and a defined policy for account linking once social login is introduced.

## Tests and CI

- [ ] There is no test runner, test suite, Playwright configuration, or CI workflow.
- [ ] Add Playwright at the workspace root with an isolated Postgres test database. Start the Fastify API and Vite app from the Playwright configuration; apply migrations before tests and reset state between tests.
- [ ] Cover the core browser flows: public home health state, signup, duplicate signup, login failure, logout, `/settings` redirect-back, profile/password updates, and signed-in redirects away from `/login` and `/signup`.
- [ ] When Google login is implemented, test only the app-owned initiation/redirect behavior in CI. Keep the real Google consent/callback flow as a protected staging smoke test rather than a normal PR test.
- [ ] Add fast server/integration coverage for auth session handling and public/protected tRPC procedures.
- [ ] Add CI for install, format, lint, typecheck, build, dependency audit, migrations, and the E2E suite.

## Reproducibility and deployment

- [x] The root README documents local installation, environment files, database commands, development commands, and a production migration policy.
- [ ] Fix the Compose mapping from `5432:${DB_PORT}` to `${DB_PORT}:5432`; the configured host port currently has no effect. Rename the stale `finance_tracker_db` volume at the same time if a clean development volume is acceptable.
- [ ] Add production runtime/deployment configuration (for example Dockerfiles and static-web serving guidance). Compose only runs PostgreSQL; it does not deploy the API or web app.
- [ ] Add a distinct test database configuration before introducing E2E tests; never run browser tests against the development database.

## Quality-check snapshot

- [x] `pnpm typecheck` passes.
- [x] `pnpm build` passes.
- [ ] `pnpm lint` fails. The web config cannot resolve `tooling/eslint/react.ts`'s extensionless `./base` ESM import, and `packages/api/src/index.ts` has five rule violations.
- [ ] `pnpm format` fails for `apps/server/tsconfig.json`, `apps/server/turbo.json`, `apps/web/src/components/ui/radio-group.tsx`, and `apps/web/src/components/ui/scroll-area.tsx`.
- [ ] Runtime/database checks were not rerun in this audit because the local Docker daemon was unavailable. They need to be exercised against a newly migrated database.

## Cleanup and maintenance

- [ ] Fix or remove the unused `getAuthErrorMessage`; it returns `{ en: string }` rather than a display string.
- [ ] Change `CurrencyField` from invalid `type="string"` to `type="text"` with `inputMode="decimal"`.
- [ ] Close the PostgreSQL pool during Fastify shutdown instead of relying on forced `process.exit`.
- [ ] Remove or implement empty database modules (`migrate.ts`, `seed.ts`, and `schemas/settings.ts`) so the package does not imply nonexistent behavior.
- [ ] Remove stale product references: `apps/web/README.md` still describes a finance tracker; the root README lists nonexistent `.vscode`, `packages/ui`, and TanStack Table; `apps/web/index.html` is titled `web`; and the Compose volume retains a finance-tracker name.
