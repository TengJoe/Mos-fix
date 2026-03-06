[中文](./fork-fix-log-2026-03-05.zh-CN.md) | [English](./fork-fix-log-2026-03-05.md)

# Fork 修复日志（2026-03-05）

这个日志记录了分支 `codex/fix-cvdisplaylink-crash` 上已实现的修复。

## 1) 滚动时闪退（CVDisplayLink 线程）

- 对应 issue：https://github.com/Caldis/Mos/issues/868
- 根因：
  跨线程使用由回调持有的 `CGEvent`，可能触发无效生命周期问题。
- 修复：
  在 `ScrollPoster.update(...)` 中，存储前立即复制传入事件：
  - `Mos/ScrollCore/ScrollPoster.swift`

## 2) UU 远程桌面双重平滑

- 对应 issue：https://github.com/Caldis/Mos/issues/879
- 根因：
  `UU Remote Desktop` 的 bundle id 不在远控应用白名单中。
- 修复：
  将 `com.netease.uuremote` 添加到 `REMOTE_CONTROL_APPLICATION.bundleIdentifiers`：
  - `Mos/Utils/Constants.swift`

## 3) Dock 文件夹中滚动效果失效（反转/平滑未生效）

- 对应 issues：
  - https://github.com/Caldis/Mos/issues/851
  - https://github.com/Caldis/Mos/issues/878
- 根因：
  Dock 目标被无条件视为 Launchpad，导致平滑/反转逻辑被跳过。
- 修复：
  收紧 Launchpad 检测逻辑，仅在实际检测到 Launchpad 窗口（`LPSpringboard` / `Launchpad`）时禁用效果，而不是对所有 Dock 场景都禁用：
  - `Mos/ScrollCore/ScrollUtils.swift`

## 4) iPhone 镜像反转滚动兼容性

- 对应 issues：
  - https://github.com/Caldis/Mos/issues/655
  - https://github.com/Caldis/Mos/issues/871
- 修改：
  将 `com.apple.ScreenContinuity` 加入特殊事件源 bundle id，并把事件源匹配从单值改成列表：
  - `Mos/Utils/Constants.swift`
  - `Mos/ScrollCore/ScrollEvent.swift`

## 验证说明

- 当前环境中的本地 `xcodebuild` 验证已可完成，不再受只有 Command Line Tools 的限制。
- 运行时验证仍建议在真实设备和实际工作流中完成：
  - 2.4G 鼠标在 Dock 文件夹栈/网格中的滚动
  - iPhone Mirroring 中的反转滚动
  - UU 远程桌面主机/客户端同时启用 Mos 的场景
