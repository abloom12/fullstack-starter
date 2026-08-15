# Tasks completed

- **Removed Polar integration:** Deleted the auth plugin module and removed its configuration, signup hooks, server wiring, and environment variable. Package and lockfile cleanup remains intentionally deferred.
- **Completed minimal email auth flow:** Added a protected settings route, public home with logout, validated email forms, settings redirect-back, default home redirects, and signed-in redirects away from auth pages.
- **Documented local setup:** Added prerequisites, environment setup, database bootstrap, development commands, quality checks, and production migration guidance to the root README.
- **Built basic settings:** Added current account/session details, profile name and image URL updates, password changes without revoking other sessions, and sign-out.
