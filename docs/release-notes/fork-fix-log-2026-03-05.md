# Fork Fix Log (2026-03-05)

This log records fixes implemented on fork branch `codex/fix-cvdisplaylink-crash`.

## 1) Crash while scrolling (CVDisplayLink thread)
- Related issue: https://github.com/Caldis/Mos/issues/868
- Root cause:
  Cross-thread use of callback-owned `CGEvent` could hit an invalid lifetime.
- Fix:
  In `ScrollPoster.update(...)`, copy the incoming event immediately before storing it:
  - `Mos/ScrollCore/ScrollPoster.swift`

## 2) UU Remote Desktop double-smoothing
- Related issue: https://github.com/Caldis/Mos/issues/879
- Root cause:
  `UU Remote Desktop` bundle id was missing from remote-control app allowlist.
- Fix:
  Added `com.netease.uuremote` to `REMOTE_CONTROL_APPLICATION.bundleIdentifiers`:
  - `Mos/Utils/Constants.swift`

## 3) Dock folder scrolling effects disabled (reverse/smooth not applied)
- Related issues:
  - https://github.com/Caldis/Mos/issues/851
  - https://github.com/Caldis/Mos/issues/878
- Root cause:
  Dock target was treated as Launchpad unconditionally, so smoothing/reverse logic was skipped.
- Fix:
  Refined Launchpad detection to only disable effects when Launchpad window is actually present (`LPSpringboard` / `Launchpad`), not for all Dock contexts:
  - `Mos/ScrollCore/ScrollUtils.swift`

## 4) iPhone Mirroring reverse scroll compatibility
- Related issues:
  - https://github.com/Caldis/Mos/issues/655
  - https://github.com/Caldis/Mos/issues/871
- Change:
  Added `com.apple.ScreenContinuity` to special event-source bundle ids and generalized source matching from single value to list:
  - `Mos/Utils/Constants.swift`
  - `Mos/ScrollCore/ScrollEvent.swift`

## Validation notes
- Local `xcodebuild` validation is blocked in current environment because only Command Line Tools are active (`xcodebuild` requires full Xcode).
- Runtime validation should be done on macOS with real devices/workflows:
  - 2.4G mouse scrolling in Dock folder stack/grid
  - iPhone Mirroring reverse scrolling
  - UU Remote Desktop host/client both with Mos enabled
