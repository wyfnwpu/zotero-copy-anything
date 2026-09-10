# Changelog

本项目源自原作者 **windfollowingheart** 的
[zotero-copy-anything](https://github.com/windfollowingheart/zotero-copy-anything)
项目。以下记录的是本仓库的修改内容。

## 1.0.10 - 2026-09-10

### Fixed

- 修复 Zotero 10 顶部 PDF 标签页右键菜单中的 `Copy` 不显示问题。
- 移除会被 Zotero 10 Fluent 本地化机制清空的动态 `l10nID`，改为在菜单弹出时设置实际标签。
- 为顶部标签页菜单使用插件专属的注册 ID。
- 对菜单上下文中的空条目进行过滤，避免无效附件导致复制命令异常。

### Compatibility

- 兼容范围上限调整为 Zotero `10.*`。
- 重新整理主窗口 FTL 资源注入和右键菜单注册流程。
- 修复 Zotero 10 下不存在的辅助程序路径调用 `PathUtils.normalize()` 导致初始化失败的问题。

## 1.0.9 - 2026-09-10

- 增加 Zotero 10 顶部标签页菜单注册。
- 修复插件版本覆盖问题并重新构建安装包。

## Upstream history

更早的版本历史请参考原作者项目：

<https://github.com/windfollowingheart/zotero-copy-anything>
