[中文](./FORK_NOTES.zh-CN.md) | [English](./FORK_NOTES.md)

# Fork Notes

This fork now tracks upstream `Mos 4.0.1` and only keeps the changes that are still fork-specific after upstream absorbed the crash and remote-desktop fixes from `4.0.0`.

## Summary

This fork currently focuses on:

- improving reverse-scroll compatibility in iPhone Mirroring
- keeping stricter Dock / Launchpad detection for pre-macOS-26 Dock folder and stack scenarios
- labeling in-app builds as `TengJoe Codex Fix`
- providing clickable Chinese / English doc variants for readers

Detailed implementation notes live in [docs/release-notes/fork-fix-log-2026-03-08.md](docs/release-notes/fork-fix-log-2026-03-08.md).
Release-ready notes live in [docs/release-notes/4.0.1-20260308.1-tengjoe-codexfix.md](docs/release-notes/4.0.1-20260308.1-tengjoe-codexfix.md).

## Remaining fork-specific patches

### 1. iPhone Mirroring compatibility

- Scope: reverse scrolling inside iPhone Mirroring
- Fork change: `com.apple.ScreenContinuity` is treated as a special event source and shares the same non-trackpad classification path as Logitech Options+
- Effect: improves reverse-scroll behavior when events originate from iPhone Mirroring

### 2. Dock folder and stack protection

- Scope: Dock right-side folders, stacks, and similar Dock-hosted scrolling views on systems where Launchpad still shares Dock process behavior
- Fork change: Dock is no longer treated as Launchpad unconditionally; Launchpad suppression only applies when Launchpad windows are actually present
- Effect: reduces false positives that disable smoothing/reverse logic in Dock folder contexts

## Upstream status

Upstream `4.0.1` already includes:

- the `CVDisplayLink` / cross-thread scroll-posting crash fix
- UU Remote Desktop support
- a macOS 26+ Launchpad skip

This fork therefore no longer carries the old crash patch separately.
