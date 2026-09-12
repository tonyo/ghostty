# ADR 0001: macOS configurable tab background colors

## Status

Proposed

## Context

Ghostty on macOS supports per-tab accent colors shown as a small dot in the tab accessory view. Users have reported that this dot is too subtle and that the default active/inactive tab backgrounds are hard to tell apart, especially with `macos-titlebar-style = tabs` and macOS Reduce Transparency enabled (discussions #3189, #12174).

We need a way for users to configure the background color and opacity of active and inactive tabs.

## Decision

Add four new macOS-only configuration options:

- `macos-titlebar-tab-active-color`
- `macos-titlebar-tab-active-opacity`
- `macos-titlebar-tab-inactive-color`
- `macos-titlebar-tab-inactive-opacity`

When unset, Ghostty keeps the current automatic tab coloring. When set, the values override the automatic colors for the tab background fill.

### Scope boundaries

- Applies only to `macos-titlebar-style = tabs`. Native AppKit tabs and the `transparent` titlebar style are out of scope because they use different rendering paths and offer far less customization surface.
- Within `tabs`, the initial implementation targets the Ventura code path (`TitlebarTabsVenturaTerminalWindow`, macOS 13–15). The Tahoe path (`TitlebarTabsTahoeTerminalWindow`, macOS 26+) uses a different tab-bar layout and is not yet covered.
- Separate `color` and `opacity` keys follow the existing Ghostty convention used by `background`/`background-opacity` and `cursor-color`/`cursor-opacity`.
- Per-tab colors remain independent and continue to render as the existing accessory-view dot; they do not blend with or override the active/inactive background.
- Only the resting active and inactive background colors are configurable; foreground text and hover/pressed states are out of scope.
- Config changes apply live to existing windows.

## Consequences

- Users can make active and inactive tabs visually distinct.
- The feature is intentionally narrow: macOS-only, `tabs` style only, background only.
- Future work (e.g., `colorize_tab` input binding in #11085) remains orthogonal because per-tab colors are still rendered as the dot.
- If we later want to support `transparent` or native titlebar styles, we will need separate ADRs because the implementation mechanisms differ significantly.
