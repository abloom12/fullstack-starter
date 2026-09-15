# Fullstack Starter Simplification Plan

## Goal

Finish this repository as a small, reliable private scaffold that can be cloned, initialized, verified, and adapted without first removing unfinished platform features.

This document is the source of truth for the remaining work. The older review-remediation documents are reference material only and should be removed after any useful details have been incorporated here.

## Target starter

Keep:

- React and Vite;
- TanStack Router, Query, and Form;
- Fastify and tRPC;
- Drizzle and PostgreSQL;
- Better Auth email/password authentication and sessions;
- signup, login, logout, profile update, and password update;
- one public and one protected tRPC procedure;
- the UI components used by current routes.

Remove or defer:

- Google OAuth;
- admin, organization, two-factor, OpenAPI, and Have I Been Pwned auth plugins;
- email verification and password reset;
- application CRUD examples such as todos;
- unreachable UI components and unused form controls;
- unnecessary frontend devtools and unused dependencies;
- production Docker images, hosting configuration, and reverse-proxy guidance;
- public distribution and open-source licensing work.

## Working rules

- Prefer deleting unused code over repairing or documenting it.
- Do not add features to justify existing dependencies or scaffolding.
- Keep every workspace package private.
- Commit one minimal initial migration so a fresh clone works immediately.
- Use incremental migrations after the initial migration is committed; do not rewrite migration history once data must be preserved.
- Keep provider-specific deployment concerns outside the starter.
- Add tests only for the starter's core contracts.

## Execution plan

### 1. Reduce application scope

- [ ] Remove advanced Better Auth plugins and their options.
- [ ] Remove Google OAuth environment variables and server wiring.
- [ ] Remove matching Better Auth client plugins.
- [ ] Remove plugin-only auth tables, columns, and relations.
- [ ] Remove unused auth error-code scaffolding.
- [ ] Delete unreachable UI components and `use-mobile.ts`.
- [ ] Retain only the form fields used by current routes.
- [ ] Remove unnecessary devtools from the application.
- [ ] Remove dependencies made unused by the cleanup.
- [ ] Confirm signup, login, logout, profile update, and password update still work.

### 2. Upgrade and stabilize dependencies

- [ ] Upgrade Better Auth and its schema tooling together.
- [ ] Upgrade Fastify and compatible Fastify plugins.
- [ ] Upgrade Vite, Turbo, and other direct dependencies with known advisories.
- [ ] Remove duplicate or unused adapter packages instead of upgrading them.
- [ ] Refresh and commit the pnpm lockfile.
- [ ] Confirm a frozen install succeeds.
- [ ] Require zero critical or high production dependency advisories.

### 3. Make the database reproducible

- [ ] Finalize the minimal core auth schema after the Better Auth upgrade.
- [ ] Make schema generation use a version compatible with the installed Better Auth runtime.
- [ ] Fix database environment loading without relying on a missing `dotenv` executable.
- [ ] Simplify root database scripts to call the database package directly.
- [ ] Correct the Docker Compose port mapping and remove stale product naming.
- [ ] Add PostgreSQL readiness checking for local startup.
- [ ] Generate, review, and commit one initial migration.
- [ ] Verify the migration on a new PostgreSQL 17 database.
- [ ] Verify running migrations a second time is safe.

### 4. Make runtime behavior safe

- [ ] Use readable logging in development and structured JSON logging in production.
- [ ] Ensure production never attempts to load `pino-pretty`.
- [ ] Retain the PostgreSQL pool and close it through a Fastify shutdown hook.
- [ ] Remove immediate successful-path `process.exit()` calls.
- [ ] Validate browser environment variables.
- [ ] Reject the public example auth secret in production.
- [ ] Confirm the built API starts in production mode, serves health requests, and exits cleanly on `SIGTERM`.

### 5. Make quality checks truthful and green

- [ ] Change the web typecheck so it checks application and Vite source files.
- [ ] Align Turbo typecheck outputs with the generated TypeScript build-info files.
- [ ] Fix the shared ESLint ESM import.
- [ ] Allow TanStack Router's expected `Route` export without broadly disabling React Refresh linting.
- [ ] Resolve remaining lint findings without weakening strict rules.
- [ ] Format the repository.
- [ ] Confirm clean runs of `pnpm format`, `pnpm lint`, `pnpm typecheck`, and `pnpm build`.

### 6. Fix core browser contracts

- [ ] Correct password visibility button labels.
- [ ] Add stable `name` attributes to auth controls.
- [ ] Add appropriate `autocomplete` values to auth and settings fields.
- [ ] Verify labels, descriptions, and errors reference the correct controls.
- [ ] Confirm keyboard-only use of signup, login, and password update.

### 7. Add lean tests and CI

- [ ] Add small Fastify tests for public health and anonymous protected access.
- [ ] Test clean server initialization and shutdown.
- [ ] Add a disposable PostgreSQL migration test.
- [ ] Add one Playwright journey covering signup, protected settings, logout, redirect protection, and login.
- [ ] Add a production-mode API startup and shutdown smoke test.
- [ ] Add CI for frozen install, format, lint, typecheck, build, production dependency audit, migrations, tests, and smoke checks.
- [ ] Block critical and high production dependency advisories without requiring a broad exception system.

### 8. Finish repository cleanup

- [ ] Add `private: true` to every internal workspace package.
- [ ] Delete empty and misleading database modules.
- [ ] Remove stale finance-product and template references.
- [ ] Correct the application title and repository structure documentation.
- [ ] Rewrite the root README around the verified setup and commands.
- [ ] Clearly identify the repository as a private reusable scaffold.
- [ ] Remove superseded remediation documents.
- [ ] Run the complete verification sequence from a clean checkout.

## Required verification

Before calling the starter finished, verify:

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

Also verify that:

- a new PostgreSQL 17 database initializes from the committed migration;
- the migration command is safe to run again;
- the browser auth journey passes;
- the production-mode API starts, responds to health requests, and shuts down cleanly;
- no tracked source, documentation, package, or dependency exists solely for a deferred feature.

## Definition of done

- A fresh clone installs with the frozen lockfile.
- Local PostgreSQL becomes ready and initializes through the documented commands.
- Core email/password authentication works end to end.
- Public and protected tRPC behavior is tested.
- Production-mode startup and shutdown work without development dependencies.
- Format, lint, typecheck, build, migration, test, and security gates pass in CI.
- The codebase and README describe only the intentionally supported starter scope.
