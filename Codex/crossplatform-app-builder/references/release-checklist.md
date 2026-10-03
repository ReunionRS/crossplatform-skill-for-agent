# Localization, Verification, and Release

Read this reference when adding languages, changing platform configuration, preparing a build, deploying, or handling credentials.

## Localization

Use Flutter's localization pipeline (`flutter_localizations`, `intl`, ARB files, and generated delegates) rather than hand-written string maps for production UI. Give keys semantic names and preserve interpolation, plural, and select behavior.

Translate visible UI, validation, empty/error/loading states, dialogs, tooltips, and accessibility labels. Persist a supported locale identifier and fall back predictably when a locale is not supported by Flutter's Material/Cupertino delegates. A selector without a translated reachable interface is incomplete.

## Minimum verification matrix

Choose checks proportionate to the change, normally including:

```text
flutter pub get
dart format --set-exit-if-changed .
flutter analyze
flutter test
flutter build web
```

Add Android/iOS builds when their configuration or behavior changed and the host supports them. Exercise affected Firebase flows against an emulator or controlled project with more than one identity for collaborative permissions.

For UI work, verify compact and wide layouts, light and dark themes, empty/loading/error/data states, keyboard/focus behavior, and the reported reproduction path.

## Configuration and secrets

- Keep environment-specific configuration out of reusable business logic.
- Do not commit service-account JSON, private keys, CI tokens, signing keys, `.env` files, or generated artifacts containing private values.
- Firebase web API keys are client-visible configuration, not authentication secrets. Protect the backend with Auth, Firestore/Storage rules, API restrictions, authorized domains, quotas, and App Check where appropriate.
- Scan the tracked tree and relevant Git history before claiming a leaked value was removed. Rotate truly secret credentials.
- Provide a tracked example/template only when it contains no real credentials.

## Release sequence

1. Confirm the selected Firebase/project environment and intended targets.
2. Run analysis, tests, and requested platform builds while preserving unrelated user changes.
3. Review the staged diff for generated files, secrets, and environment drift.
4. Deploy only authorized targets with explicit project selection.
5. Open the deployed URL, confirm its version, and execute the critical path.
6. Report commit/deployment identifiers and any console-side setup still required.

Stop retries when failure requires new credentials, billing, console authorization, or a product decision; report the exact blocker instead of weakening security or validation.
