[中文](./FORK_NOTES.zh-CN.md) | [English](./FORK_NOTES.md)

# Fork 说明

这个 fork 现在跟随上游 `Mos 4.0.1`，只保留在上游已吸收 `4.0.0` 那批修复之后仍然属于 fork 自己的改动。

## 概览

当前主要保留：

- 改善 iPhone 镜像中的反转滚动兼容性
- 在 macOS 26 之前保留更严格的 Dock / Launchpad 区分逻辑
- 在应用内标注 `TengJoe Codex Fix`
- 为读者提供可点击切换的中英文文档

详细实现日志见：

- [docs/release-notes/fork-fix-log-2026-03-08.zh-CN.md](docs/release-notes/fork-fix-log-2026-03-08.zh-CN.md)
- [docs/release-notes/4.0.1-20260308.1-tengjoe-codexfix.zh-CN.md](docs/release-notes/4.0.1-20260308.1-tengjoe-codexfix.zh-CN.md)

## 仍由 fork 保留的补丁

### 1. iPhone 镜像兼容性

- 范围：iPhone 镜像中的反转滚动
- fork 修改：将 `com.apple.ScreenContinuity` 视作特殊事件源，并走与 Logitech Options+ 相同的非触控板分类路径
- 效果：改善 iPhone Mirroring 里的反转滚动行为

### 2. Dock 文件夹与叠放视图保护

- 范围：Dock 右侧文件夹、叠放视图等 Dock 内滚动区域，尤其是 Launchpad 仍与 Dock 进程耦合的系统版本
- fork 修改：不再把 Dock 无条件视作 Launchpad，只有真正检测到 Launchpad 窗口时才屏蔽相关效果
- 效果：减少 Dock 文件夹场景下平滑/反转逻辑被误伤

## 上游状态

上游 `4.0.1` 已经包含：

- `CVDisplayLink` / 跨线程滚动投递崩溃修复
- UU 远程桌面支持
- macOS 26+ 的 Launchpad 跳过逻辑

因此这个 fork 不再单独携带旧的闪退补丁。
