---
name: crossplatform-app-builder
description: Build, debug, adapt, and release Flutter applications that share one codebase across web and mobile. Use for responsive Flutter UI, Firebase Auth/Firestore realtime data, permissions, localization, platform configuration, testing, and deployment; do not use for native-only Android, iOS, or unrelated web stacks.
---

# Cross-platform App Builder

Own the observable outcome on every requested platform. Inspect the repository, its instructions, current state, and existing architecture before editing. Preserve unrelated work and the user's chosen stack.

## Work from evidence

1. Translate the request into acceptance checks by platform, viewport, user role, connectivity state, and persistence boundary.
2. Trace the actual screen, state owner, repository/service call, Firestore path and rule before changing code. Reproduce defects at the reported width or interaction speed when practical.
3. Reuse existing widgets, theme tokens, models, services, streams, routes, and platform configuration. Prefer Flutter and Firebase native capabilities to parallel custom abstractions.
4. Make the smallest cohesive change that fixes the shared contract rather than a platform-specific visual symptom.
5. Verify the integrated diff with static analysis, relevant tests, builds, and targeted UI checks. A source-pattern check is not proof of runtime behavior.

Keep authentication, permissions, validation, accessibility, error visibility, and data integrity intact. Ask only when a missing product choice materially changes the result or requires new authority.

## Route only the needed detail

- For responsive structure, theme contrast, navigation, dialogs, interaction, and Flutter lifecycle/state failures, read [adaptive-ui.md](references/adaptive-ui.md).
- For Firebase Auth, Firestore schema/rules, realtime sharing, presence, contacts, tasks, media, and configuration, read [firebase-realtime.md](references/firebase-realtime.md).
- For localization, automated checks, web/mobile builds, deployment, and secret hygiene, read [release-checklist.md](references/release-checklist.md).

Do not load all references for a narrow task.

## Non-negotiable invariants

- One source of truth owns each piece of shared state; screens observe it instead of copying it.
- Queries, document shape, and security rules must agree. Test allowed and denied paths with at least two identities when access is collaborative.
- Realtime listeners must have stable lifecycles. Do not recreate streams or controllers from `build` unless the framework API explicitly expects it.
- Responsive behavior is structural, not a scaled desktop screenshot. Keep essential controls reachable at adjacent widths and with the on-screen keyboard open.
- Theme colors come from the active `ColorScheme`; verify contrast in light and dark themes, including overlays on user-selected backgrounds.
- Never solve configuration by committing private service credentials. Firebase web configuration is client-visible by design, but it still requires API restrictions, authorization rules, and secret scanning.
- A release is complete only after the requested target builds and the deployed behavior is reachable when deployment is in scope.

## Report completion

State what behavior changed, which platforms and roles were checked, the commands or runtime flows that passed, and any remaining external setup such as Firebase console configuration. Stop when the requested behavior and evidence are complete.
