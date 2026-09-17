---
id: TASK-011
title: Clean up the README and old docs
status: To Do
assignee: []
created_date: '2026-09-15 02:33'
updated_date: '2026-09-15 13:04'
labels: []
dependencies:
  - TASK-010
references:
  - docs/simplification-plan.md
modified_files:
  - README.md
  - apps/web/README.md
  - apps/web/index.html
  - .dockerignore
  - docs
priority: high
type: docs
ordinal: 11000
---

## Description

<!-- SECTION:DESCRIPTION:BEGIN -->
Update the repository documentation after the code and CI are finished. The README should explain the starter as it actually works, and old finance, template, audit, and remediation notes should be removed instead of maintained.
<!-- SECTION:DESCRIPTION:END -->

## Acceptance Criteria
<!-- AC:BEGIN -->
- [ ] #1 The root README calls this a private reusable scaffold and matches the existing license.
- [ ] #2 The README documents the tested install, env setup, database setup, dev, quality-check, test, and production-mode commands.
- [ ] #3 The README lists only features and directories that exist; Google, advanced auth, finance, TanStack Table, .vscode, and packages/ui references are gone.
- [ ] #4 apps/web has a meaningful page title, the finance-specific web README is removed, and .dockerignore refers to apps/server rather than apps/api.
- [ ] #5 Copied vendor notes and superseded audit, completed-task, and review-remediation docs are removed.
- [ ] #6 No tracked source, docs, package, or dependency remains only for a feature we deferred.
- [ ] #7 From a clean checkout, frozen install, format, lint, typecheck, build, production audit, migrations, API tests, Playwright, and the production smoke all pass.
<!-- AC:END -->

## Definition of Done
<!-- DOD:BEGIN -->
- [ ] #1 Acceptance criteria are met
- [ ] #2 Relevant tests and quality checks pass
- [ ] #3 Documentation is updated when behavior or setup changes (if documentation exists)
<!-- DOD:END -->
