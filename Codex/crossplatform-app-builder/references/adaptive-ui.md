# Adaptive Flutter UI

Read this reference for layout, navigation, theme, interaction, or widget lifecycle work.

## Start with the interaction contract

Record the affected widths and states before editing: empty, loading, error, populated, selected, keyboard open, light theme, and dark theme. Use content pressure rather than a device name to choose a breakpoint.

Typical chat structure:

- Compact: one surface at a time; list → conversation → information, with back navigation.
- Medium: chat list plus conversation; information opens as a sheet or route.
- Wide: independently scrollable list, conversation, and information panes.

Use `LayoutBuilder` or `MediaQuery.sizeOf` at the layout owner. Do not scatter unrelated width checks through leaf widgets. Preserve scroll ownership for every pane and constrain dialogs and sheets on wide displays.

## Stable state and lifecycle

- Create streams, controllers, focus nodes, animation controllers, and subscriptions in a stable owner (`initState`, provider, bloc, repository) and dispose them there.
- Rapid navigation must not replace a valid list with an empty transient state. Keep the last good data while refreshing when that matches product intent.
- Guard async UI work with mounted/lifecycle checks. Cancel stale requests or ignore results that no longer belong to the active selection.
- Treat framework assertions as lifecycle evidence: find which dependency, key, focus node, controller, or route survives beyond its owner instead of hiding the exception.
- Avoid nested unconstrained scroll views. In columns, give scrollable content a bounded area such as `Expanded`.

## Interaction parity

Provide equivalent input paths:

- Mouse: click, hover, context menu, drag and drop.
- Touch: tap, long press, drag, and appropriately sized targets.
- Keyboard: focus order, Enter/Escape behavior, and shortcuts only where discoverable.

For draggable task cards, persist order/status only after a valid drop, show a visible destination, and recover the original position on failure. Keep mutation logic outside the draggable widget.

## Theme and backgrounds

Derive text, icons, dividers, surfaces, disabled states, and semantic colors from the active theme. Do not use hardcoded black text or low-opacity foregrounds that disappear in dark mode.

On user-selected images, insert a theme-aware scrim between the background and content. Cards may be translucent, but text and icons must remain legible on both bright and dark regions. Verify controls without relying on tooltips; the icon itself must be visible.

## Targeted acceptance

Check the reported width plus one narrower and one wider width. Exercise rapid switching, refresh, back navigation, keyboard opening, dialog dismissal, scrolling, and theme switching. When visual regressions matter, capture before/after screenshots at the same dimensions.
