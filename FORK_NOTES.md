# Fork Notes

This fork keeps upstream `Mos 4.0.0` as the base and adds a small set of targeted fixes for stability and compatibility.

## Summary

This fork currently focuses on:

- reducing the scrolling crash risk around `CVDisplayLink`
- restoring smooth/reverse scrolling in Dock folder and stack views
- improving reverse-scroll compatibility in iPhone Mirroring
- avoiding double smoothing in UU Remote Desktop sessions

Detailed implementation notes live in [docs/release-notes/fork-fix-log-2026-03-05.md](docs/release-notes/fork-fix-log-2026-03-05.md).

## Fixes in this fork

### 1. Scrolling crash mitigation

- Scope: unexpected app exits while scrolling
- Upstream issue: `#868`
- Change: the scroll event is copied before it crosses from the event callback into the display-link driven posting path
- Effect: lowers the chance of invalid event lifetime usage and related crashes

### 2. Dock folder smooth/reverse scrolling

- Scope: Dock right-side folders, stacks, or similar Dock-hosted scrolling views
- Upstream issues: `#851`, `#878`
- Change: Launchpad detection was narrowed so Dock is no longer treated as Launchpad unconditionally
- Effect: reverse scrolling and smooth scrolling can keep working in Dock folder contexts

### 3. iPhone Mirroring compatibility

- Scope: reverse scrolling inside iPhone Mirroring
- Upstream issues: `#655`, `#871`
- Change: `com.apple.ScreenContinuity` was added as a special event source and the source matching logic was generalized from a single identifier to a list
- Effect: improves reverse-scroll behavior when events originate from iPhone Mirroring

### 4. UU Remote Desktop compatibility

- Scope: remote sessions where both sides use Mos
- Upstream issue: `#879`
- Change: `com.netease.uuremote` was added to the remote-control application list
- Effect: avoids double smoothing and the resulting over-acceleration or unstable scroll feel

## Positioning

This fork is not a feature fork. It is a maintenance fork intended to make daily use more stable in a few high-friction scenarios.

If you want the code-level details, read:

- [docs/release-notes/fork-fix-log-2026-03-05.md](docs/release-notes/fork-fix-log-2026-03-05.md)

## 中文说明

这个 fork 基于上游 `Mos 4.0.0`，重点做了几项定向修复，不是功能分叉版。

当前主要修复点：

- 降低滚动时闪退概率
- 恢复 Dock 文件夹/叠放视图中的平滑与反转滚动
- 改善 iPhone 镜像中的反转滚动兼容性
- 避免 UU 远程桌面双重平滑

详细修复日志见：

- [docs/release-notes/fork-fix-log-2026-03-05.md](docs/release-notes/fork-fix-log-2026-03-05.md)
