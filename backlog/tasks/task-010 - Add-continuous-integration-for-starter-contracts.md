---
id: TASK-010
title: Add continuous integration for starter contracts
status: To Do
assignee: []
created_date: '2026-09-15 02:33'
labels: []
dependencies:
  - TASK-008
  - TASK-009
references:
  - docs/simplification-plan.md
modified_files:
  - .github/workflows/ci.yml
  - package.json
  - turbo.json
priority: high
type: chore
ordinal: 10000
---

## Description

<!-- SECTION:DESCRIPTION:BEGIN -->
The repository has no automated gate proving that a clean checkout installs, passes quality checks, initializes PostgreSQL, exercises core auth, or starts in production mode. Add one compact CI workflow using the commands established by earlier tasks so regressions in the scaffold contract block changes.
<!-- SECTION:DESCRIPTION:END -->

## Acceptance Criteria
<!-- AC:BEGIN -->
- [ ] #1 CI runs for pull requests and pushes to the main branch.
- [ ] #2 CI uses the Node and pnpm versions pinned by the repository.
- [ ] #3 CI starts a healthy isolated PostgreSQL 17 service with explicit test-only credentials.
- [ ] #4 CI performs pnpm install --frozen-lockfile before verification.
- [ ] #5 CI requires format, lint, real typecheck, and build commands to pass.
- [ ] #6 CI blocks critical and high production dependency advisories.
- [ ] #7 CI applies the committed migration to the isolated database and runs the migration verification.
- [ ] #8 CI runs server integration tests and the production startup smoke test.
- [ ] #9 CI installs Chromium and runs the single browser authentication journey.
- [ ] #10 All environment variables are explicit and CI does not depend on ignored developer env files.
- [ ] #11 The workflow contains no placeholder commands and passes from a clean checkout without relying on pre-existing Turbo caches.
<!-- AC:END -->

## Definition of Done
<!-- DOD:BEGIN -->
- [ ] #1 Acceptance criteria are met
- [ ] #2 Relevant tests and quality checks pass
- [ ] #3 Documentation is updated when behavior or setup changes (if documentation exists)
<!-- DOD:END -->
