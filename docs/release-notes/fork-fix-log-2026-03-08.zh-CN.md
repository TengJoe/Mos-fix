[中文](./fork-fix-log-2026-03-08.zh-CN.md) | [English](./fork-fix-log-2026-03-08.md)

# Fork 修复日志（2026-03-08）

这个日志记录了 rebase 到上游 `Mos 4.0.1` 之后，fork 仍然保留的差异。

## 1) iPhone 镜像反转滚动兼容性

- 范围：iPhone 镜像中的反转滚动
- fork 修改：
  将 `com.apple.ScreenContinuity` 加入特殊事件源 bundle id，并把事件源匹配逻辑从单值改成列表。
- 文件：
  - `Mos/Utils/Constants.swift`
  - `Mos/ScrollCore/ScrollEvent.swift`

## 2) 更严格的 Dock / Launchpad 区分

- 范围：Dock 文件夹、叠放视图，以及仍可能把 Dock 与 Launchpad 混淆的系统版本
- fork 修改：
  只有真正检测到 Launchpad 窗口时才屏蔽相关效果，而不是把 Dock 无条件视作 Launchpad。
- 文件：
  - `Mos/ScrollCore/ScrollUtils.swift`

## 3) Fork 身份与读者文档

- 范围：fork 分发与读者识别
- fork 修改：
  在应用 bundle 中增加 `MosForkReleaseLabel`，并在版本文案中显示，同时加入可点击切换的中英文文档。
- 文件：
  - `Mos/Info.plist`
  - `Mos/Windows/WelcomeWindow/WelcomeViewController.swift`
  - `Mos/Windows/PreferencesWindow/UpdateView/PreferencesUpdatesViewController.swift`
  - `README.md`
  - `README.enUS.md`
  - `FORK_NOTES.md`
  - `FORK_NOTES.zh-CN.md`

## 已由上游吸收的部分

上游 `4.0.1` 已经包含：

- 滚动投递崩溃修复
- UU 远程桌面支持
- macOS 26+ 的 Launchpad 绕过逻辑

这些修复不再作为 fork 的单独补丁继续携带。
