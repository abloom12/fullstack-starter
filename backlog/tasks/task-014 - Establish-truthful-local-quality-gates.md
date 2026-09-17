---
id: TASK-014
title: Establish truthful local quality gates
status: To Do
assignee: []
created_date: '2026-09-17 00:34'
labels: []
dependencies:
  - TASK-012
  - TASK-013
documentation:
  - doc-001
ordinal: 14000
---

## Description

<!-- SECTION:DESCRIPTION:BEGIN -->
Create a reliable verification seam for subsequent dependency, database, and runtime work. The existing commands must inspect the source and tooling configuration they claim to validate.
<!-- SECTION:DESCRIPTION:END -->

## Acceptance Criteria
<!-- AC:BEGIN -->
- [ ] #1 Web typechecking covers application source and Vite configuration.
- [ ] #2 A temporary TypeScript error in application source fails web and root typechecking.
- [ ] #3 Executable TypeScript tooling configuration is covered by an appropriate no-emit typecheck.
- [ ] #4 Turbo tracks the TypeScript build-information outputs actually produced by each workspace.
- [ ] #5 The shared React ESLint configuration loads in its ESM environment.
- [ ] #6 TanStack Router’s expected Route export is allowed without globally disabling React Refresh checks.
- [ ] #7 Generated route code is the only application source excluded from linting.
- [ ] #8 Remaining lint findings are resolved without weakening strict rules.
- [ ] #9 From clean caches, format, lint, typecheck, and build all pass.
<!-- AC:END -->

## Definition of Done
<!-- DOD:BEGIN -->
- [ ] #1 Acceptance criteria are met
- [ ] #2 Relevant tests and quality checks pass
- [ ] #3 Documentation is updated when behavior or setup changes (if documentation exists)
<!-- DOD:END -->
