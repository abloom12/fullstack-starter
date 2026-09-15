---
id: TASK-003
title: Make local quality gates truthful
status: To Do
assignee: []
created_date: '2026-09-15 02:32'
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
The repository currently reports misleading quality results: the web typecheck selects no application files, ESLint cannot load the shared React configuration, known API and frontend findings remain hidden, and formatting is red. Repair the quality tooling after obsolete auth and frontend source has been removed so subsequent upgrades are evaluated against trustworthy checks.
<!-- SECTION:DESCRIPTION:END -->

## Acceptance Criteria
<!-- AC:BEGIN -->
- [ ] #1 The web typecheck selects both application source and Vite configuration source.
- [ ] #2 A deliberate temporary TypeScript error in web source causes both the web and root typecheck commands to fail during verification.
- [ ] #3 Turbo typecheck outputs match the build-info files actually produced and generate no missing-output warning.
- [ ] #4 The shared React ESLint configuration resolves correctly under the pinned Node version.
- [ ] #5 TanStack Router route modules may export Route while React Refresh checks remain enabled for other exports.
- [ ] #6 Generated route code is excluded without broadly ignoring application source.
- [ ] #7 Known API and retained web lint findings are resolved without weakening strict rules.
- [ ] #8 pnpm format, pnpm lint, pnpm typecheck, and pnpm build pass from clean local caches.
<!-- AC:END -->

## Definition of Done
<!-- DOD:BEGIN -->
- [ ] #1 Acceptance criteria are met
- [ ] #2 Relevant tests and quality checks pass
- [ ] #3 Documentation is updated when behavior or setup changes (if documentation exists)
<!-- DOD:END -->
