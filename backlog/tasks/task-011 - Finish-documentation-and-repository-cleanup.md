---
id: TASK-011
title: Finish documentation and repository cleanup
status: To Do
assignee: []
created_date: '2026-09-15 02:33'
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
The repository documentation and metadata still describe stale product features, nonexistent directories, and unverified setup behavior. Once CI proves the final scaffold contract, reduce documentation to accurate project-specific guidance, remove superseded review material, and verify the same workflow from a clean checkout.
<!-- SECTION:DESCRIPTION:END -->

## Acceptance Criteria
<!-- AC:BEGIN -->
- [ ] #1 The root README identifies the repository as a private reusable scaffold consistent with its license.
- [ ] #2 The README documents the verified prerequisites, environment setup, PostgreSQL bootstrap, development commands, quality checks, tests, and production-mode boundary.
- [ ] #3 The README describes only implemented features and contains no Google, advanced-auth, finance-product, TanStack Table, nonexistent .vscode, or nonexistent packages/ui claims.
- [ ] #4 The documented repository structure matches tracked source.
- [ ] #5 The web application has a meaningful starter title instead of web.
- [ ] #6 The stale finance-specific web README and incorrect Docker ignore references are removed or corrected.
- [ ] #7 Copied vendor notes without a clear project-specific maintenance purpose are removed.
- [ ] #8 Superseded audit, completed-task, and review-remediation documents are removed after useful requirements are represented by Backlog tasks or current docs.
- [ ] #9 No tracked source, documentation, package, or dependency exists solely for a deferred feature.
- [ ] #10 A clean-checkout run passes frozen install, format, lint, typecheck, build, production audit, migrations, server tests, browser tests, and production smoke.
<!-- AC:END -->

## Definition of Done
<!-- DOD:BEGIN -->
- [ ] #1 Acceptance criteria are met
- [ ] #2 Relevant tests and quality checks pass
- [ ] #3 Documentation is updated when behavior or setup changes (if documentation exists)
<!-- DOD:END -->
