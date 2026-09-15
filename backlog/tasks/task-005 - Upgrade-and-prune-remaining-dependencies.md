---
id: TASK-005
title: Upgrade and prune remaining dependencies
status: To Do
assignee: []
created_date: '2026-09-15 02:32'
labels: []
dependencies:
  - TASK-004
references:
  - docs/simplification-plan.md
modified_files:
  - package.json
  - pnpm-workspace.yaml
  - pnpm-lock.yaml
  - apps/server/package.json
  - apps/web/package.json
  - packages/api/package.json
  - packages/auth/package.json
  - packages/db/package.json
priority: high
type: chore
ordinal: 5000
---

## Description

<!-- SECTION:DESCRIPTION:BEGIN -->
The production dependency graph contains critical and high advisories, duplicate adapter declarations, packages retained only by deleted source, and inconsistent internal package metadata. Upgrade the remaining dependency families against the repaired quality gates, remove packages that no longer have a justified use, and establish a reproducible security baseline without broad overrides.
<!-- SECTION:DESCRIPTION:END -->

## Acceptance Criteria
<!-- AC:BEGIN -->
- [ ] #1 Fastify and its plugins are upgraded to mutually compatible releases that include available security fixes.
- [ ] #2 Vite, Turbo, and other direct build dependencies with known fixes are upgraded compatibly.
- [ ] #3 Unused separate Better Auth adapter declarations are removed.
- [ ] #4 Dependencies made unused by authentication and frontend cleanup are removed.
- [ ] #5 Development-only tooling is not classified as a production runtime dependency.
- [ ] #6 Every internal workspace package is marked private unless deliberate publishing configuration exists.
- [ ] #7 The lockfile is refreshed without audit --fix --force or permanent broad security overrides.
- [ ] #8 pnpm install --frozen-lockfile succeeds after the refreshed lockfile is committed.
- [ ] #9 pnpm audit --prod --audit-level high reports no critical or high production advisories.
- [ ] #10 Any remaining lower-severity finding has a concise applicability and follow-up record.
- [ ] #11 Format, lint, typecheck, and build gates remain green.
<!-- AC:END -->

## Definition of Done
<!-- DOD:BEGIN -->
- [ ] #1 Acceptance criteria are met
- [ ] #2 Relevant tests and quality checks pass
- [ ] #3 Documentation is updated when behavior or setup changes (if documentation exists)
<!-- DOD:END -->
