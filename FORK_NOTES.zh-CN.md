[中文](./FORK_NOTES.zh-CN.md) | [English](./FORK_NOTES.md)

# Fork 说明

这个 fork 基于上游 `Mos 4.0.0`，重点做了几项定向修复，不是功能分叉版。

## 概览

当前主要修复点：

- 降低 `CVDisplayLink` 相关滚动闪退概率
- 恢复 Dock 文件夹和叠放视图中的平滑与反转滚动
- 改善 iPhone 镜像中的反转滚动兼容性
- 避免 UU 远程桌面双重平滑

详细实现日志见：

- [docs/release-notes/fork-fix-log-2026-03-05.zh-CN.md](docs/release-notes/fork-fix-log-2026-03-05.zh-CN.md)
- [docs/release-notes/4.0.0-20260220.1-tengjoe-codexfix.zh-CN.md](docs/release-notes/4.0.0-20260220.1-tengjoe-codexfix.zh-CN.md)

## 修复内容

### 1. 滚动闪退缓解

- 范围：滚动时应用意外退出
- 对应上游 issue：`#868`
- 修改：在事件从回调线程进入 display-link 驱动的发送路径前，先复制滚动事件
- 效果：降低无效事件生命周期导致的崩溃概率

### 2. Dock 文件夹平滑/反转滚动修复

- 范围：Dock 右侧文件夹、叠放视图等 Dock 内滚动区域
- 对应上游 issues：`#851`、`#878`
- 修改：收窄 Launchpad 检测逻辑，不再把所有 Dock 场景都视作 Launchpad
- 效果：Dock 文件夹场景下可继续使用平滑滚动和反转滚动

### 3. iPhone 镜像兼容性

- 范围：iPhone 镜像中的反转滚动
- 对应上游 issues：`#655`、`#871`
- 修改：将 `com.apple.ScreenContinuity` 加入特殊事件源列表，并把事件源匹配逻辑从单值扩展为列表
- 效果：改善 iPhone Mirroring 里的反转滚动行为

### 4. UU 远程桌面兼容性

- 范围：远程主机与客户端都使用 Mos 的场景
- 对应上游 issue：`#879`
- 修改：将 `com.netease.uuremote` 加入远控应用列表
- 效果：避免双重平滑带来的过度加速或滚动手感异常

## 定位

这个 fork 不是功能分叉版，而是一个偏维护型的 fork，目标是在几个高频问题场景里提升日常使用稳定性。

如果你需要看更细的代码层说明，见：

- [docs/release-notes/fork-fix-log-2026-03-05.zh-CN.md](docs/release-notes/fork-fix-log-2026-03-05.zh-CN.md)
