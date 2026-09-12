# Ghostty Tab Appearance — Domain Glossary

## Terms

- **Tab**: The visual tab item in the macOS tab bar when `macos-titlebar-style = tabs` is active. Not the small colored indicator dot, not the right-click context menu, not the Window menu list, and not the native AppKit tab bar.
- **Active tab**: The currently selected/focused tab in a tab group.
- **Inactive tab**: Any unselected tab in the same tab group.
- **Tab background color**: The fill color of the entire tab shape behind its title.
- **Tab opacity**: The alpha level of that fill. Distinct from window `background-opacity`.
- **Per-tab color**: The user-assigned accent color shown for a single tab. Today this is a 6 px dot in the tab accessory view.

## Decisions

- The new settings apply only to `macos-titlebar-style = tabs`. Native tabs and `transparent` titlebar style are out of scope.
- Settings are exposed as separate color and opacity keys, matching existing Ghostty conventions (`background` + `background-opacity`).
- When unset, today's auto-derived tab colors remain unchanged.
- Per-tab colors continue to be shown only as the accessory-view dot; they do not blend into or override the active/inactive tab background.
- Only the tab background is configurable; tab title foreground and hover/pressed states are out of scope.
- Changing the settings must update existing windows live.
