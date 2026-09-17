---
id: TASK-013
title: Make authentication forms browser-correct
status: To Do
assignee: []
created_date: '2026-09-17 00:34'
labels: []
dependencies: []
documentation:
  - doc-001
ordinal: 13000
---

## Description

<!-- SECTION:DESCRIPTION:BEGIN -->
Harden the retained authentication and settings forms while preserving every reusable component and development overlay. Nothing in the reusable component inventory, nor its required support code or dependencies, may be removed merely because current routes do not import it.
<!-- SECTION:DESCRIPTION:END -->

## Acceptance Criteria
<!-- AC:BEGIN -->
- [ ] #1 Input and password controls derive stable id and name values from their field names.
- [ ] #2 Input and password controls accept typed autocomplete values.
- [ ] #3 Login, signup, profile, and password fields use the applicable email, name, current-password, and new-password autocomplete values.
- [ ] #4 Labels, descriptions, and validation errors reference the correct controls.
- [ ] #5 Password visibility controls use type="button" and announce “Show password” or “Hide password” according to their state.
- [ ] #6 Signup, login, and password-update interactions can be completed using only the keyboard.
- [ ] #7 The web application builds with the complete reusable component inventory and development overlays retained.
<!-- AC:END -->

## Definition of Done
<!-- DOD:BEGIN -->
- [ ] #1 Acceptance criteria are met
- [ ] #2 Relevant tests and quality checks pass
- [ ] #3 Documentation is updated when behavior or setup changes (if documentation exists)
<!-- DOD:END -->
