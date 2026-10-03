<div align="center">
  <img src="assets/openai-logo.png" width="520" alt="OpenAI logo">

  # Cross-platform App Builder for Codex

  A practical Codex Skill for building a single Flutter application for web and mobile.

  **English** · [Русский](README.ru.md)
</div>

## What this skill does

- designs adaptive Flutter interfaces instead of merely scaling a desktop layout;
- diagnoses lifecycle errors, unstable streams, and race conditions during rapid navigation;
- aligns Firebase Auth, Firestore schemas, realtime listeners, roles, and Security Rules;
- supports shared chats, contacts, groups, and task boards with consistent permissions;
- preserves accessible contrast across light and dark themes and user-selected backgrounds;
- implements internationalization with ARB files and Flutter localization delegates;
- verifies, builds, and releases web/mobile applications without exposing private credentials.

The workflow adapts the evidence-led approach from `mega-orchestrator`: reproduce the actual state and trace its data source first, then make the smallest cohesive change and verify the resulting application.

## Structure

```text
Codex/
└── crossplatform-app-builder/
    ├── SKILL.md
    ├── agents/openai.yaml
    └── references/
        ├── adaptive-ui.md
        ├── firebase-realtime.md
        └── release-checklist.md
```

## Install in Codex

```powershell
git clone https://github.com/ReunionRS/crossplatform-skill-for-agent.git
Copy-Item -Recurse .\crossplatform-skill-for-agent\Codex\crossplatform-app-builder "$env:CODEX_HOME\skills\crossplatform-app-builder"
```

If `CODEX_HOME` is not defined, use `%USERPROFILE%\.codex\skills\crossplatform-app-builder`. Restart Codex after copying the skill.

Invoke it explicitly with:

```text
$crossplatform-app-builder Fix the adaptive chat layout on web and mobile, then verify the Firestore permissions.
```

The skill also supports automatic selection for matching tasks.

## Technologies

<p>
  <img src="https://cdn.simpleicons.org/flutter/02569B" height="34" alt="Flutter">
  <img src="https://cdn.simpleicons.org/dart/0175C2" height="34" alt="Dart">
  <img src="https://cdn.simpleicons.org/firebase/DD2C00" height="34" alt="Firebase">
  <img src="https://cdn.simpleicons.org/android/3DDC84" height="34" alt="Android">
  <img src="https://cdn.simpleicons.org/apple/000000" height="34" alt="Apple">
  <img src="https://cdn.simpleicons.org/googlechrome/4285F4" height="34" alt="Web">
</p>

## Usage notice

This skill provides instructions for Codex. It does not contain the source code of a particular application, a Firebase project, or credentials. Review generated changes, access rules, and the selected environment before a production deployment.

OpenAI and Codex are trademarks of their respective owners. This repository is an independent community project and is not an official OpenAI product.
