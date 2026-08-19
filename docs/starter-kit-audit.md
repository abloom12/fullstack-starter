# Starter Kit Audit & TODOs

This audit reflects the current source tree and the quality checks run locally.

## Release blockers

- [ ] **Commit an initial Drizzle migration.** `packages/db/src/migrations/` exists but is empty. A fresh database has no auth tables, so the documented `pnpm db:migrate` bootstrap cannot create them. Generate, review, commit, and apply the initial migration before relying on signup or deploying.
- [x] **Fix the server environment example.** It now includes the required `HOST` and a development-only `BETTER_AUTH_SECRET` placeholder that satisfies the enforced 32-character minimum. Replace the secret with a generated value before deployment.
- [ ] **Upgrade vulnerable dependencies.** `pnpm audit --prod` reports 37 vulnerabilities: 2 critical, 26 high, 6 moderate, and 3 low. In particular, the locked Better Auth `1.6.8` is vulnerable (the audit identifies `>=1.6.22` as patched), and Vite `8.0.9` is below the audit's patched `8.0.16`. Update direct packages and compatible transitive dependencies, then rerun the audit and the full auth flow.
- [x] **Hide unavailable Google sign-in.** Google configuration is optional and the provider is registered only when both server credentials are set. The no-op controls have been removed; add a control only when `authClient.signIn.social({ provider: 'google' })` and the Google OAuth callback are configured.

## Auth and application flow

- [x] Email/password signup, sign-in, sign-out, session-aware home, and redirect-back to `/settings` are implemented.
- [x] `/settings` is protected by a route-level session check.
- [x] Client password validation matches the configured 12–128-character server policy.
- [x] The auth server validates its environment, uses explicit CORS origins with credentials, rate limiting, Helmet, and Better Auth trusted origins.
- [ ] Evolve Settings into the self-service account area: profile, password, email verification, linked accounts, active-session list/revocation, 2FA, and account deletion. Split it into routes such as `/settings/profile`, `/settings/security`, and `/settings/danger` as it grows.

## Better Auth feature roadmap

- [ ] **Add transactional email first.** Configure verification and password-reset delivery, add the associated screens and resend/retry states, then require verified email where appropriate.
- [ ] **Finish two-factor authentication in Settings/Security.** Add TOTP enrollment/verification, backup-code display and regeneration, disable/recovery flows, and E2E coverage for sign-in with 2FA.
- [ ] **Finish organizations in a separate route area.** Add `/organizations`, `/organizations/:slug`, and member, invitation, role, team, and organization-settings screens. Include an organization switcher and server/E2E authorization coverage for every membership boundary.
- [ ] **Finish administration in a separate restricted route area.** Add `/admin`, `/admin/users`, and other global-management screens for user listing, role changes, bans, and session/account actions. Do not combine this with organization management.
- [ ] **Enforce authorization on the server.** UI visibility is not access control: every organization procedure must check membership/organization role, and every admin procedure must check the global admin role. Add denial tests for ordinary users and members of other organizations.
- [ ] **Document the feature contracts.** State the account-linking, email-verification, invitation, recovery, retention, and support policies before exposing these workflows to users.

## Starter-template reference experience

- [ ] **Add one complete protected CRUD feature.** Use a small, user-owned resource such as notes, projects, or tasks to demonstrate the intended vertical slice: Drizzle schema and migration, Zod validation, protected tRPC query/mutation, React Query invalidation, form handling, and empty/loading/error states. The current API demonstrates health and auth but not a feature pattern consumers can copy.
- [ ] **Build a shared application shell.** Add authenticated navigation, a user menu, settings/sign-out access, and consistent not-found, route-error, and loading states. Link Settings for all signed-in users, Organizations when available, and Admin only for admins; this should wrap the reference feature rather than remain an isolated auth demo.
- [ ] **Keep the template intentionally scoped.** Prefer a polished email/password baseline and the reference feature over enabled-but-unimplemented integrations. Keep Google optional, and only retain admin, organization, and 2FA when the template includes their supported workflows.
- [ ] **Add useful local seed data once the reference feature exists.** Replace the empty seed module with an idempotent development seed and document how to run it; never use it for production data.

## Tests and CI

- [ ] There is no test runner, test suite, Playwright configuration, or CI workflow.
- [ ] Add Playwright at the workspace root with an isolated Postgres test database. Start the Fastify API and Vite app from the Playwright configuration; apply migrations before tests and reset state between tests.
- [ ] Cover the core browser flows: public home health state, signup, duplicate signup, login failure, logout, `/settings` redirect-back, profile/password updates, signed-in redirects away from `/login` and `/signup`, and the reference feature's CRUD lifecycle.
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
