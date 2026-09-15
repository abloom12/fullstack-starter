---
id: TASK-002
title: Prune unused frontend code and harden retained auth forms
status: To Do
assignee: []
created_date: '2026-09-15 02:07'
labels: []
dependencies: []
references:
  - docs/simplification-plan.md
modified_files:
  - apps/web/src/App.tsx
  - apps/web/src/lib/form.ts
  - apps/web/src/components/form
  - apps/web/src/components/ui
  - apps/web/src/hooks
  - apps/web/src/routes/login.tsx
  - apps/web/src/routes/signup.tsx
  - apps/web/src/routes/_app/settings.tsx
priority: high
type: chore
ordinal: 2000
---

## Description

<!-- SECTION:DESCRIPTION:BEGIN -->
The frontend retains unreachable UI primitives, speculative form controls, and development overlays. This increases bundle size and maintenance while obscuring issues in the small set of forms the scaffold supports.

Delete the known unreachable social-auth, dialog/menu/overlay/sidebar/tab/toggle components and use-mobile hook. Remove unused checkbox, currency, native-select, select, and textarea form controls, followed by any UI primitives that become unreachable. Harden only the retained signup, login, profile, and password controls. Package-manifest and lockfile pruning, Playwright coverage, browser environment validation, and global quality-tool configuration are handled by later tasks.
<!-- SECTION:DESCRIPTION:END -->

## Acceptance Criteria
<!-- AC:BEGIN -->
- [ ] #1 The form hook registers only InputField, PasswordField, and SubmitButton.
- [ ] #2 Every retained non-generated frontend component is reachable from the application entry point or route tree.
- [ ] #3 The application renders no TanStack or React Query development overlays.
- [ ] #4 Text and password controls expose id and name using the field name.
- [ ] #5 Retained controls accept a type-safe autoComplete value.
- [ ] #6 Login uses email and current-password autocomplete values.
- [ ] #7 Signup uses name, email, and new-password autocomplete values.
- [ ] #8 Password update uses current-password for the current password and new-password for both new-password fields.
- [ ] #9 A hidden password announces Show password and a visible password announces Hide password.
- [ ] #10 Password visibility controls use type="button" and remain keyboard-operable.
- [ ] #11 Labels, descriptions, and errors reference the correct control IDs.
- [ ] #12 The web production build succeeds.
- [ ] #13 A fresh source import-graph check finds no remaining unreachable UI or form modules.
<!-- AC:END -->

## Definition of Done
<!-- DOD:BEGIN -->
- [ ] #1 Acceptance criteria are met
- [ ] #2 Relevant tests and quality checks pass
- [ ] #3 Documentation is updated when behavior or setup changes (if documentation exists)
<!-- DOD:END -->
