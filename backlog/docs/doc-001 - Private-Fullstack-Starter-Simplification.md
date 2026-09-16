---
id: doc-001
title: Private Fullstack Starter Simplification
type: specification
created_date: '2026-09-16 17:31'
updated_date: '2026-09-16 17:32'
---
# Private Fullstack Starter Simplification

## Problem

The repository contains unfinished platform features, unused frontend scaffolding, unreliable development and production behavior, and quality checks that do not fully validate the application. A fresh clone cannot yet be treated as a small, reproducible scaffold without first removing unsupported features or repairing setup, migration, and runtime behavior.

The starter needs to describe and verify only the functionality it intentionally supports.

## Intended Outcome

Produce a small, reliable, private fullstack scaffold that can be cloned, initialized, tested, and adapted without removing unfinished product features first.

The completed starter provides:

- React and Vite with TanStack Router, Query, and Form;
- Fastify and tRPC;
- Drizzle and PostgreSQL 17;
- Better Auth email/password authentication and sessions;
- signup, login, logout, profile update, and password update;
- one public and one protected tRPC procedure;
- only the UI, packages, dependencies, and documentation needed by the supported scope;
- reproducible database initialization from a committed migration;
- safe development, test, and production runtime behavior;
- truthful local quality commands and CI verification.

## User Stories

1. As a developer, I can clone the repository, install from the frozen lockfile, initialize a fresh local database, and start the application using documented commands.
2. As a user, I can sign up with email and password, log in, access protected settings, update my profile and password, log out, and log back in.
3. As an operator, I can build and start the API in production mode, receive structured logs, verify its public health procedure, and stop it cleanly with `SIGTERM`.
4. As a maintainer, I can rely on local and CI checks to validate formatting, linting, type safety, builds, migrations, core API behavior, the browser authentication journey, production startup, and production dependency security.

## Requirements and Invariants

### Supported scope

- Every workspace package must remain private.
- The supported authentication model is email/password authentication with sessions.
- Authentication must continue to support signup, login, logout, profile updates, and password changes.
- The tRPC API must retain:
  - the public `health.ping` procedure;
  - the protected `health.me` procedure;
  - an `UNAUTHORIZED` result from `health.me` when no valid session is present.
- UI retained in the repository must be reachable from the application route tree or required by a retained route.
- No tracked source, documentation, package, or dependency may exist solely for a deferred feature.

### Authentication simplification

- Google OAuth and its environment configuration, server wiring, client wiring, and documentation must be removed.
- Admin, organization, two-factor, OpenAPI, and Have I Been Pwned Better Auth plugins must be removed.
- Plugin-specific synthetic user fields, client plugins, error-code scaffolding, database tables, columns, and relations must be removed.
- Core authentication creation must require only the database, application origin, authentication URL, and secret.
- Email verification and password-reset workflows must not be presented as supported features.

### Frontend simplification and browser contracts

- Unreachable UI components, unused hooks, unused form controls, social-auth UI, and frontend development overlays must be removed.
- The shared form setup must retain only the input, password, and submit controls used by current routes.
- Retained input and password controls must:
  - derive stable `id` and `name` attributes from the field name;
  - accept typed autocomplete values;
  - associate labels, descriptions, and errors with the correct control.
- Authentication and settings fields must use appropriate `email`, `name`, `current-password`, and `new-password` autocomplete values.
- Password visibility controls must use `type="button"` and announce:
  - “Show password” while the password is hidden;
  - “Hide password” while the password is visible.
- Signup, login, and password-update interactions must be usable with a keyboard alone.

### Dependencies and package hygiene

- Better Auth and its schema tooling must use the same reviewed, lockfile-pinned version.
- Authentication schema generation must not use `pnpm dlx`, an unpinned package, or an `@latest` version.
- Fastify, compatible Fastify plugins, Vite, Turbo, and other direct dependencies with applicable security fixes must be upgraded compatibly.
- Duplicate adapters, unused UI packages, unused development tools, and dependencies made unnecessary by simplification must be removed rather than retained or upgraded.
- Development-only build and test tooling must not be production dependencies.
- Dependency changes must update the committed pnpm lockfile.
- A frozen-lockfile installation must succeed.
- The production dependency graph must contain no known critical or high advisories.
- Forced audit fixes and broad dependency overrides must not be used to conceal advisories.

### Database reproducibility

- The final schema must represent only core email/password authentication requirements.
- The authentication schema generator must:
  - use explicit core email/password configuration;
  - operate without a live database connection or production environment values;
  - fail if generation produces an empty or missing schema.
- The generated authentication schema must contain only the required user, session, account, and verification tables and their required relations.
- Admin, organization, invitation, member, two-factor, ban, role, impersonation, and active-organization data must not remain.
- Root database commands must work without relying on a missing standalone `dotenv` executable.
- An explicitly supplied `DATABASE_URL` must take precedence over values loaded from local environment files.
- Local Docker Compose configuration must:
  - run PostgreSQL 17;
  - map the configured host database port to container port `5432`;
  - use starter-neutral resource names;
  - expose readiness through a passing `pg_isready` health check.
- Empty or misleading migration, seed, settings, and schema modules must be removed.
- One reviewed initial Drizzle migration and its metadata must be committed.
- A new PostgreSQL 17 database must initialize successfully from the committed migration.
- Running the migration command a second time against that database must be safe.
- After the initial baseline is committed, schema evolution must use incremental migrations rather than rewriting migration history that may protect existing data.

### Runtime safety

- Development logging must be human-readable.
- Test construction must permit logging to be disabled.
- Production logging must be structured JSON and must not load `pino-pretty`.
- Validated server configuration must distinguish development, test, and production modes.
- Browser API URL configuration must be validated before use and produce a clear startup or build failure when missing or invalid.
- The server must reject the public example authentication secret in production.
- The PostgreSQL pool must remain available for the server lifetime and be closed through the Fastify shutdown lifecycle.
- `SIGINT` and `SIGTERM` must initiate shutdown no more than once.
- Successful shutdown must complete naturally rather than immediately invoking `process.exit()`.
- The built API must start with production dependencies, serve `health.ping`, and exit successfully after `SIGTERM`.

### Quality gates

- Web typechecking must cover application source and Vite configuration.
- Introducing a temporary TypeScript error in web application source must cause both web and root typecheck commands to fail.
- Turbo must track the TypeScript build-information outputs actually produced by the workspaces.
- The shared React ESLint configuration must load correctly in an ESM environment.
- Route modules may use TanStack Router’s expected `Route` export without disabling React Refresh checks globally.
- Generated route code must be the only application source excluded from linting.
- Remaining lint findings must be resolved without weakening strict rules.
- From clean caches, the following commands must pass:

```bash
pnpm format
pnpm lint
pnpm typecheck
pnpm build
```

### Documentation and repository consistency

- The repository must be described as a private reusable scaffold consistent with its proprietary license.
- The application must have a meaningful, starter-neutral browser title.
- Documentation must describe the verified install, environment setup, database setup, development, quality, test, migration, and production-mode commands.
- Documentation must list only features and directories that exist.
- Google OAuth, advanced authentication, finance-product, TanStack Table, nonexistent editor configuration, and nonexistent shared UI-package references must be removed.
- Superseded audits, remediation plans, completed-task notes, copied vendor notes, and obsolete product-specific documentation must be removed.
- Provider-specific hosting, reverse-proxy, and deployment guidance must not be introduced.

## Implementation Decisions

- Preserve the existing monorepo architecture and the selected React, Vite, TanStack, Fastify, tRPC, Better Auth, Drizzle, and PostgreSQL technologies.
- Better Auth schema generation uses the same pinned Better Auth version as the runtime and a dedicated configuration representing only supported email/password options.
- Tests for server behavior use the Node test runner through TypeScript execution rather than introducing a separate test framework or mock-heavy architecture.
- API behavior is tested through Fastify application construction without opening a network port.
- Browser behavior is tested through Playwright using Chromium.
- Production startup is tested against the built server and a production dependency installation.
- Local PostgreSQL remains containerized for development and verification, while production images and provider-specific deployment assets remain outside the starter.
- Migrations, rather than schema push operations, are the reproducible database contract.

## Testing Decisions

The highest practical public seams are:

1. **Fastify/tRPC application seam**
   - Construct the Fastify application without listening on a network port.
   - Verify successful `health.ping`.
   - Verify anonymous `health.me` returns `UNAUTHORIZED`.
   - Always close Fastify and PostgreSQL resources.
   - Typecheck server tests without emitting them into the production build.

2. **Database migration seam**
   - Use a disposable PostgreSQL 17 database.
   - Apply the committed migration successfully.
   - Apply migrations a second time to prove rerun safety.

3. **Browser seam**
   - Run one serial Playwright Chromium journey with explicit test environment values and a disposable database.
   - Sign up a unique user and reach protected settings.
   - Log out and confirm direct settings access redirects to login.
   - Log in with the same account and reach settings again.
   - Ensure application processes are stopped on both success and failure.
   - Typecheck Playwright configuration and tests.

4. **Built production-process seam**
   - Use the built API with production dependencies and production configuration.
   - Wait for `health.ping` to succeed.
   - Send `SIGTERM`.
   - Require exit code `0`.
   - Clean up the child process if verification fails.
   - Do not rely on `pino-pretty`.

5. **Clean-checkout CI seam**
   - Run for pull requests and pushes to `main`.
   - Use the Node and pnpm versions pinned by the repository.
   - Start a healthy PostgreSQL 17 service with test-only credentials.
   - Supply all test environment variables without local ignored environment files.
   - Run frozen installation, formatting, linting, typechecking, building, production dependency auditing, migration verification, API tests, the production startup smoke check, and the Playwright journey.
   - Pass without relying on a pre-existing Turbo cache or placeholder commands.

Root commands must expose the API tests, browser tests, and production smoke check. The complete verification sequence must include:

```bash
pnpm install --frozen-lockfile
pnpm format
pnpm lint
pnpm typecheck
pnpm build
pnpm audit --prod --audit-level high
pnpm db:migrate
pnpm test
pnpm test:e2e
```

## Out of Scope

- Google or other social authentication providers.
- Admin, organization, two-factor, OpenAPI, or breached-password Better Auth plugins.
- Email verification and password-reset workflows.
- Application CRUD examples such as todos.
- UI controls and components not used by retained routes.
- Broad frontend or backend test suites beyond the starter’s core contracts.
- Production Docker images.
- Hosting-provider configuration, reverse-proxy guidance, and other provider-specific deployment concerns.
- Public package distribution, open-source release preparation, or licensing changes.

## Further Notes

The committed initial migration establishes the reusable baseline for fresh clones. Once that baseline may protect real data, future schema changes must be additive or incremental migrations rather than edits to migration history.
