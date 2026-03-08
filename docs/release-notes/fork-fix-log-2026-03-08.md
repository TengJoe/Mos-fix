[中文](./fork-fix-log-2026-03-08.zh-CN.md) | [English](./fork-fix-log-2026-03-08.md)

# Fork Fix Log (2026-03-08)

This log records the fork-only delta after rebasing onto upstream `Mos 4.0.1`.

## 1) iPhone Mirroring reverse-scroll compatibility

- Scope: reverse scrolling inside iPhone Mirroring
- Fork change:
  Added `com.apple.ScreenContinuity` to the special event-source bundle identifiers and generalized the matching logic from a single identifier to a list.
- Files:
  - `Mos/Utils/Constants.swift`
  - `Mos/ScrollCore/ScrollEvent.swift`

## 2) Stricter Dock / Launchpad distinction

- Scope: Dock folders, stacks, and related Dock-hosted views on systems where Dock and Launchpad can still be conflated
- Fork change:
  Launchpad suppression now applies only when Launchpad windows are actually present, instead of treating Dock as Launchpad unconditionally.
- File:
  - `Mos/ScrollCore/ScrollUtils.swift`

## 3) Fork identity and reader docs

- Scope: fork distribution and reader clarity
- Fork change:
  Added `MosForkReleaseLabel` to the app bundle, surfaced it in version labels, and added clickable Chinese / English doc variants.
- Files:
  - `Mos/Info.plist`
  - `Mos/Windows/WelcomeWindow/WelcomeViewController.swift`
  - `Mos/Windows/PreferencesWindow/UpdateView/PreferencesUpdatesViewController.swift`
  - `README.md`
  - `README.enUS.md`
  - `FORK_NOTES.md`
  - `FORK_NOTES.zh-CN.md`

## Upstream overlap removed

Upstream `4.0.1` already includes:

- the scroll-posting crash fix
- UU Remote Desktop support
- a macOS 26+ Launchpad workaround

Those fixes are no longer carried as separate fork patches here.
