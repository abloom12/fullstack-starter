---
id: TASK-003
title: 'Fix typecheck, lint, and formatting'
status: To Do
assignee: []
created_date: '2026-09-15 02:32'
updated_date: '2026-09-15 13:04'
labels: []
dependencies:
  - TASK-001
  - TASK-002
references:
  - docs/simplification-plan.md
modified_files:
  - apps/web/package.json
  - apps/web/tsconfig.json
  - apps/web/tsconfig.app.json
  - apps/web/tsconfig.node.json
  - apps/web/eslint.config.js
  - tooling/eslint/react.ts
  - packages/api/src/index.ts
  - turbo.json
priority: high
type: chore
ordinal: 3000
---

## Description

<!-- SECTION:DESCRIPTION:BEGIN -->
Make the existing quality commands tell the truth and pass. The web typecheck currently checks zero source files, web lint cannot load the shared React config, and formatting is red.

Do this after TASK-001 and TASK-002 so we do not spend time fixing files that should be deleted.
<!-- SECTION:DESCRIPTION:END -->

## Acceptance Criteria
<!-- AC:BEGIN -->
- [ ] #1 The web typecheck checks both app source and vite.config.ts instead of selecting zero files.
- [ ] #2 A temporary TypeScript error under apps/web/src makes both the web and root typecheck commands fail.
- [ ] #3 Turbo tracks the TypeScript build-info files that are actually created and reports no missing outputs.
- [ ] #4 The shared React ESLint config loads correctly, and route files may export Route without disabling React Refresh checks everywhere.
- [ ] #5 Generated route code is the only application source excluded from lint.
- [ ] #6 All remaining API and web lint errors are fixed without turning off strict rules.
- [ ] #7 pnpm format, pnpm lint, pnpm typecheck, and pnpm build pass from clean caches.
<!-- AC:END -->

## Definition of Done
<!-- DOD:BEGIN -->
- [ ] #1 Acceptance criteria are met
- [ ] #2 Relevant tests and quality checks pass
- [ ] #3 Documentation is updated when behavior or setup changes (if documentation exists)
<!-- DOD:END -->
