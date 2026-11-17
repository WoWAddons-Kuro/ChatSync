# Changelog

## Unreleased (WoW Forever)

### Now runs on WoW Forever (Interface 16001, Mainline UI code)

- **Fixed: channels and message types silently not applying.** The Mainline UI replaced the
  `ChatFrame_AddMessageGroup` / `ChatFrame_AddChannel` family of functions with methods on the
  chat frame. ChatSync now calls whichever the client has, so profiles restore filters on both
  Classic Era and Forever. Auto-save hooks the new methods too.
- **Tab order is saved and restored.** Previously only "docked or not" was kept, so reordered
  tabs came back in window-number order.
- **Lock state and "make uninteractable"** are now applied (they were saved but ignored).
- **Floating window position is resolution-independent.** Uses the game's own screen-fraction
  position store, so a layout saved at one resolution / UI scale lands correctly on a character
  using another.
- **Chat text colors sync.** The per-chat-type colors (Say, Guild, Whisper, ...) and the
  "color names by class" flags are part of the profile now.
- **Stray windows are closed.** Applying a profile closes extra custom windows the character has
  that the profile doesn't (General / Combat Log / Voice are never closed).
- New windows are created without Blizzard's default filter set, so nothing leaks into them.
- **Edit Mode HUD layout follows the profile.** The profile remembers which Edit Mode layout
  was active (by name) and selects it on apply. Account layouts and the Modern / Classic presets
  work; character-specific layouts can't exist on other characters and are left alone. Changing
  layout on a syncing character re-saves the profile.

### Chat pings

- **Pings are off by default** now (previously whispers pinged out of the box). Existing
  settings are kept.
- The **new-character popup** has Whisper / Guild / Party ping toggles right in it, so you can
  decide about sounds while picking a layout. Sound choice and custom channels stay in `/cs`.

### Don't sync certain channels

- New **Don't sync channels** picker next to the ping channel picker. Tick a channel and it is
  never written into a profile and never added or removed when a profile is applied - meant for
  password-protected channels that addons join on their own (the game gives addons no way to
  detect a password, so this is a manual list).

Profiles saved by older versions are flagged "re-save" (they lack tab order and colors); the
usual prompt offers to update them from the current character.

## 1.2.0

### Patch 1.15.9 brought Edit Mode to Classic

- **The main chat window's position and size now come from Edit Mode.** The patch put the main
  window under Edit Mode's control, so it overrode whatever your profile set - which is why it
  stopped following your layout after the patch. Rather than fight it, ChatSync now leaves that
  one window to Edit Mode. Edit Mode layouts are **shared across your whole account**, so the
  main window already carries between characters on its own: set it once and you're done.
- **Everything else still comes from your profile,** exactly as before - tab names, docking,
  channels, message types, colours, transparency, font size, and the position and size of any
  **undocked** windows. Edit Mode doesn't touch any of that.

### Fixes

- **Settings open again.** Clicking Settings did nothing and threw an error - 1.15.9 changed how
  addons open their options page, and it now needs a numeric category ID rather than a name.
- Opening settings **during combat** no longer throws a "blocked" error. The game protects the
  options panel in combat, so ChatSync now just says to try again after the fight.
- Updated for game version **1.15.9**.

## 1.1.0

### Chat message pings
- Hear a **sound when a message comes in** — a new **Chat message pings** section in the
  settings, below your profiles.
- Pick a **sound** and click the speaker to preview it; the list also picks up sounds
  added by other addons you have installed.
- Choose what pings: **Whisper**, **Guild**, **Party**, and/or specific **custom channels**.
- Whispers ping by default, and your own messages never ping. Turn any of it off in the
  same place.

### Other
- New **What's New** window after an update, re-openable with `/cs news`.
- Settings page cleanup — aligned buttons and tidier dropdowns.

## 1.0.1

- Added a "Buy me a coffee" support link to the settings page.

## 1.0.0

- Initial release.
- Account-wide chat-window profiles: tabs, channels, message types, names, colors,
  transparency, font size, sizes and positions.
- New-character prompt to pick a profile (or auto-apply the default, or do nothing).
- Auto-update: the character a profile was saved from keeps it current on change and
  on logout; plus a one-click "Save changes" button.
- Minimap button and a settings page (`/chatsync`, `/csync`, `/cs`).
