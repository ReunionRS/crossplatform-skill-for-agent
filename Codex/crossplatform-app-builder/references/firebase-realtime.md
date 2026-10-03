# Firebase Realtime Data and Permissions

Read this reference for Firebase Auth, Cloud Firestore, presence, contacts, groups, task boards, uploads, or permission failures.

## Model collaboration explicitly

Do not infer durable product relationships from messages. Store explicit documents for contacts, group membership, roles, boards, tasks, and assignees.

A collaborative record should make authorization queryable without client joins. Depending on scale, use fields such as `ownerId`, `createdBy`, `memberIds`, or a membership subcollection. Keep one canonical permission model shared by UI, writes, queries, and rules.

| Capability | Read | Edit | Full/admin |
| --- | --- | --- | --- |
| View shared board/tasks | yes | yes | yes |
| Update permitted task fields | no | yes | yes |
| Manage members/roles or delete board | no | no | yes |

The group creator should receive the admin/full role in the same atomic creation flow. Never rely only on hidden buttons for authorization.

## Align query, data, and rules

For every failing request, write down:

1. Auth identity and expected role.
2. Exact collection/document path.
3. Query filters and ordering.
4. Existing document shape and proposed document shape.
5. Matching Firestore rule branch.

Firestore evaluates queries against their possible result set. Rules are not post-query filters. A query for shared tasks therefore needs a field or path the rules can prove belongs to the signed-in member.

Test the creator/admin, an ordinary member, an outsider, an unauthenticated user, and a malformed or privilege-escalating write.

## Realtime and connection state

Firestore snapshot listeners already provide a realtime channel. Do not add an unrelated WebSocket merely to label it “realtime.” Observe listener metadata and errors to distinguish initial connection, cached data while synchronizing, server-confirmed data, offline/retrying, and permission/configuration failure.

Keep existing data visible during a recoverable refresh. Show a persistent error or retry state when the listener fails; do not leave an endless spinner.

Presence needs an explicit contract such as `lastSeenAt` plus active session/heartbeat semantics. Calculate “online” or “was 5 minutes ago” from server timestamps with a documented freshness window. Firestore alone cannot guarantee immediate disconnect detection; choose semantics deliberately.

## Auth restoration

Wait for Firebase initialization and the first auth-state result before routing. A transient `currentUser == null` during startup must not send an authenticated user to login. Persist only non-sensitive local UI state; Firebase Auth owns the session.

## Media and Base64

Prefer Firebase Storage for normal images and store a URL plus metadata in Firestore. Use Base64 only when explicitly required and the value remains safely below Firestore's document limit after encoding overhead and all other fields. Validate MIME type, decoded size, and image dimensions; compress before encoding.

## Diagnose permission errors

Capture the failing path/query and authenticated UID first. Inspect deployed rules, not just the local file. Fix the schema/query/rule contract and add emulator or integration coverage when practical. Deploying rules and hosting are separate operations; confirm the project alias before either one.
