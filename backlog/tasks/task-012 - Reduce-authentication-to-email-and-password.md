 --
id: TASK-012
title: Reduce authentication to email and password
status: In Progress
assignee: []
created_date: '2026-09-17 00:34'
updated_date: '2026-09-18 00:44'
labels: []
dependencies: []
documentation:
  - doc-001
ordinal: 1000
---

## Description

<!-- SECTION:DESCRIPTION:BEGIN -->
Remove unsupported authentication capabilities while preserving core account and session flows. The final database schema and migration baseline are intentionally handled by the database-baseline task.
<!-- SECTION:DESCRIPTION:END -->

## Acceptance Criteria
<!-- AC:BEGIN -->
- [ ] #1 Server authentication enables only email/password authentication and sessions.
- [ ] #2 Google OAuth and the admin, organization, two-factor, OpenAPI, and breached-password plugins are absent.
- [ ] #3 Authentication configuration requires only the database, application origin, authentication URL, and secret.
- [ ] #4 Plugin-specific synthetic fields and unused authentication error scaffolding are absent.
- [ ] #5 The browser authentication client exposes only core behavior and its session and user types.
- [ ] #6 Google credentials and application wiring are absent.
- [ ] #7 Signup, login, logout, profile-update, and password-change routes retain their supported behavior.
- [ ] #8 Email verification and password-reset workflows are not exposed.
- [ ] #9 The application builds without changing the final database schema or migration history.
<!-- AC:END -->

## Definition of Done
<!-- DOD:BEGIN -->
- [ ] #1 Acceptance criteria are met
- [ ] #2 Relevant tests and quality checks pass
- [ ] #3 Documentation is updated when behavior or setup changes (if documentation exists)
<!-- DOD:END -->

## Implementation Plan

<!-- SECTION:PLAN:BEGIN -->
## Approach

Reduce Better Auth to its existing email/password and session flow by removing social-provider and advanced-plugin configuration from the server and browser client. Narrow the authentication factory inputs to the database, application origin, authentication URL, and secret.

Preserve the existing signup, login, logout, profile-update, and password-change routes unchanged. Retain all reusable components—including `social-auth-button.tsx`—because component inventory is explicitly protected; it must remain disconnected from application routes. Do not modify database schemas, migrations, package manifests, or the lockfile because dependency cleanup and the final authentication database baseline belong to subsequent tasks.

## Implementation Steps

1. Simplify `packages/auth/src/index.ts`:
   - Replace the broad, Zod-derived authentication options with a narrow type requiring only application origin, authentication URL, and secret alongside the database argument.
   - Keep email/password authentication, password limits, trusted origin handling, UUID generation, and session cookie caching.
   - Remove Google social-provider configuration; admin, organization, two-factor, OpenAPI, and breached-password plugins; plugin imports; plugin-specific synthetic user fields; production-mode input; and commented email-verification/password-reset scaffolding.
2. Update server wiring in `apps/server/src/env.ts` and `apps/server/src/app.ts`:
   - Remove Google credential validation and configuration.
   - Pass only the database, application origin, Better Auth URL, and secret into `createAuth`.
   - Preserve the server’s unrelated runtime environment validation and existing Better Auth request handler.
3. Reduce `apps/web/src/lib/auth-client.ts` to the core Better Auth React client:
   - Remove admin, organization, and two-factor client plugins.
   - Remove the unused plugin-derived error-code mapping, helper, exhaustive error-code dump, and breached-password example.
   - Continue exporting the core client and its inferred `Session` and `User` types used by the existing routes.
4. Remove Google credential examples and setup guidance from `apps/server/.env.example` and `README.md`, leaving email/password setup as the only documented authentication configuration.
5. Verify that authentication routes and reusable component inventory remain unchanged, unsupported workflows have no application routes or guidance, and database schema and migration history have not changed.

## Acceptance Criteria Coverage

- Server authentication enables only email/password authentication and sessions — `packages/auth/src/index.ts` retains only core email/password and session configuration.
- Google OAuth and advanced plugins are absent — server and client plugin imports, plugin registration, and social-provider configuration are removed and checked by scoped search.
- Authentication requires only the database, application origin, authentication URL, and secret — the narrowed `createAuth` interface and its sole call site enforce this at typecheck time.
- Synthetic fields and unused authentication error scaffolding are absent — remove `customSyntheticUser` and the unused browser error-code structures.
- The browser client exposes only core behavior and session/user types — `apps/web/src/lib/auth-client.ts` contains only `createAuthClient`, `authClient`, `Session`, and `User`.
- Google credentials and application wiring are absent — remove environment fields, server propagation, authentication provider setup, and application documentation while retaining unwired reusable component inventory.
- Supported account routes retain behavior — leave signup, login, home/logout, protected-route, and settings modules unchanged; typecheck and build their existing core-client calls.
- Email verification and password-reset workflows are not exposed — remove future-work scaffolding and ensure no application routes, controls, configuration, or setup guidance present those workflows.
- The application builds without database changes — run the repository build and confirm `packages/db` has no diff from the base branch.

## Final Verification

- `pnpm format` — verifies formatting across workspaces.
- `pnpm lint` — verifies the simplified code satisfies repository lint rules.
- `pnpm typecheck` — verifies the narrowed server factory and core browser-client contracts.
- `pnpm build` — verifies all applications and packages build together.
- `! git grep -n -I -E 'GOOGLE_CLIENT|googleClient|socialProviders|adminClient|organizationClient|twoFactorClient|haveIBeenPwned|openAPI\(|organization\(|twoFactor\(|customSyntheticUser|PASSWORD_COMPROMISED|getAuthErrorMessage' -- packages/auth/src apps/server/src apps/server/.env.example apps/web/src/lib/auth-client.ts README.md` — verifies unsupported authentication wiring and scaffolding are absent from application configuration and documentation.
- `git diff --exit-code origin/main -- packages/db` — verifies schema and migration content remains unchanged.
- `git diff --exit-code origin/main -- apps/web/src/routes apps/web/src/components` — verifies supported routes and reusable component inventory remain unchanged.
- `git diff --check` — verifies the patch contains no whitespace errors.
<!-- SECTION:PLAN:END -->
