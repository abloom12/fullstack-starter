---
id: TASK-002
title: Delete unused UI and fix auth form fields
status: To Do
assignee: []
created_date: '2026-09-15 02:07'
updated_date: '2026-09-15 13:04'
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
Delete the frontend components that are not used by the current routes. Trim the form setup to the three fields we actually use and remove the development overlays from App.

While touching the retained auth fields, add the browser attributes they are missing and fix the password visibility button. Do not remove packages or update the lockfile here; that happens in TASK-005.
<!-- SECTION:DESCRIPTION:END -->

## Acceptance Criteria
<!-- AC:BEGIN -->
- [ ] #1 All TS/TSX files that are unreachable from main.tsx and the route tree are deleted, including the social-auth button and unused dialog, menu, sidebar, tab, and toggle components.
- [ ] #2 Checkbox, currency, native-select, select, and textarea form fields are deleted along with any UI files used only by them.
- [ ] #3 apps/web/src/lib/form.ts registers only InputField, PasswordField, and SubmitButton.
- [ ] #4 apps/web/src/App.tsx no longer imports or renders TanStack or React Query development overlays.
- [ ] #5 InputField and PasswordField set both id and name from the field name and accept a typed autoComplete prop.
- [ ] #6 Login, signup, and password-change fields use the correct email, name, current-password, and new-password autocomplete values.
- [ ] #7 The password button uses type="button" and announces Show password when hidden and Hide password when visible.
- [ ] #8 pnpm --filter @acme/web build passes and a fresh import-graph scan finds no unreachable UI or form files.
<!-- AC:END -->

## Definition of Done
<!-- DOD:BEGIN -->
- [ ] #1 Acceptance criteria are met
- [ ] #2 Relevant tests and quality checks pass
- [ ] #3 Documentation is updated when behavior or setup changes (if documentation exists)
<!-- DOD:END -->
