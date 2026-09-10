# Zotero Copy Anything

一个用于 Zotero 的附件复制插件：可以把本地附件文件复制到系统剪贴板，之后直接在文件管理器、聊天软件或其他支持文件粘贴的应用中使用 `Ctrl/Cmd+V` 粘贴。

> 本项目源自原作者 **windfollowingheart** 的 [zotero-copy-anything](https://github.com/windfollowingheart/zotero-copy-anything) 项目，是在其基础上进行的 Zotero 10 兼容维护版本。原项目及本修改版本使用 AGPL-3.0-or-later 许可证。本仓库不是原作者官方发布版本，也不代表原作者对本修改版本的背书。

## 功能

- 在文献库条目右键菜单中复制附件。
- 在打开的 PDF 顶部标签页右键菜单中复制当前附件。
- 在 PDF 阅读器内容右键菜单中复制当前附件。
- 支持复制一个或多个附件。
- 支持 PDF、EPUB 以及其他可以由 Zotero 获取本地路径的附件格式。
- 支持自定义复制快捷键。
- 支持 macOS、Windows 和 Linux。

## 安装

1. 在本仓库的 GitHub **Releases** 页面下载最新的 `zotero-copy-anything.xpi`。
2. 打开 Zotero，进入“工具 → 插件”。
3. 点击右上角齿轮按钮，选择“从文件安装插件…”。
4. 选择下载的 `.xpi` 文件。
5. 完全退出并重新打开 Zotero。

插件兼容 Zotero 10。首次安装或升级后建议完整重启 Zotero，使菜单注册和辅助程序初始化重新执行。

## 使用方法

### 从文献库复制

在文献库中选中文献或附件，右键点击 `Copy`。如果选中的是文献条目，插件会复制该条目的本地附件；如果选中的是附件，则复制该附件。

### 从打开的 PDF 标签页复制

打开 PDF 后，在窗口顶部的 PDF 标签页上右键点击 `Copy`，即可复制当前打开的附件。

### 在 PDF 页面中复制

在 PDF 页面内容上右键点击 `Zotero Copy Anything`，即可复制当前阅读器中的附件。

### 设置快捷键

打开 Zotero 的插件设置页，勾选 `Enable Copy Shortcut`，然后使用 `Register Copy Shortcut` 录入快捷键并确认。阅读器处于打开状态时，快捷键优先复制当前阅读器附件；否则复制当前文献库中选中的条目。

## 首次运行与辅助程序

插件需要调用一个与操作系统对应的辅助程序。首次启动时，插件会自动下载并保存到：

```text
{ZOTERO_DATA_DIR}/storage/zotero-copy-anything
```

对应文件如下：

| 系统    | 文件名            |
| ------- | ----------------- |
| Windows | `copyfiles.exe`   |
| macOS   | `copyfiles-mac`   |
| Linux   | `copyfiles-linux` |

首次运行需要网络连接。如果自动下载失败，可以手动下载对应文件并放入上面的目录，然后重启 Zotero。

辅助程序下载地址仍使用原作者项目提供的发布地址：

- [Windows 辅助程序](https://gitee.com/windheartyolo/zotero-copy-anything/releases/download/binary/copyfiles.exe)
- [macOS 辅助程序](https://gitee.com/windheartyolo/zotero-copy-anything/releases/download/binary/copyfiles-mac)
- [Linux 辅助程序](https://gitee.com/windheartyolo/zotero-copy-anything/releases/download/binary/copyfiles-linux)

Linux 用户还需要安装 `xclip` 和 `wl-clipboard`。

## 手动启动辅助程序模式

如果 Zotero 因权限限制无法稳定调用外部程序，可以在插件设置中启用 `Manually Launch the Executable File`。

目前手动启动模式只支持 Windows。下载并启动对应的程序后，再回到 Zotero 执行复制：

- [Windows 手动启动程序](https://gitee.com/windheartyolo/zotero-copy-anything/releases/download/manual_executable/zotero-copy-anything.exe)

更多说明见 [`doc/README_manual_exe.md`](doc/README_manual_exe.md)。

## 常见问题

### 菜单中没有 `Copy`

- 确认安装的是本仓库 Releases 中的最新 `.xpi`，不要继续使用旧版本。
- 安装或升级后完全退出 Zotero，再重新打开。
- 确认当前条目或附件确实已经打开/选中。
- 在 Zotero 的“工具 → 开发者 → Error Console”中查看错误信息。

### 点击后提示复制失败

- 附件必须已经下载到本地，云端占位附件无法复制。
- 检查 `{ZOTERO_DATA_DIR}/storage/zotero-copy-anything` 中是否存在对应辅助程序。
- macOS 和 Linux 需要允许辅助程序执行；重新启动插件通常会自动设置权限。
- 如果仍然失败，尝试启用手动启动模式。

### 如何找到 Zotero 数据目录

在 Zotero 中打开“帮助 → 故障排除信息”，查看 `数据目录` 路径。

## 从源码构建

### 环境

- Node.js 和 npm
- Git
- Zotero 10（用于测试）

### 命令

```bash
npm install
npm run build
```

构建成功后，安装包位于：

```text
.scaffold/build/zotero-copy-anything.xpi
```

提交前建议运行：

```bash
npm run lint:check
git diff --check
```

### Zotero 10 兼容性修改

本维护版本主要包含以下修改：

- 将 Zotero 兼容上限调整为 `10.*`。
- 使用 Zotero 10 的 DOM/XUL 兼容接口重新注入文献库右键菜单。
- 使用 `Zotero.MenuManager` 注册顶部标签页菜单，并对 Zotero 10 的本地化覆盖行为做了标签回退处理。
- 在主窗口加载时正确注入 FTL 本地化资源。
- 修正辅助程序路径处理，避免对尚不存在的文件调用 `PathUtils.normalize()`。
- 改进辅助程序下载失败时的错误处理，避免插件初始化直接中断。

## 许可证与来源声明

本项目源自原作者 **windfollowingheart** 的 `zotero-copy-anything` 项目：

<https://github.com/windfollowingheart/zotero-copy-anything>

原项目及本修改版本使用 [GNU Affero General Public License v3.0 or later](LICENSE)。请在分发修改版时保留原项目的许可证、原作者署名和来源链接，并说明本仓库包含的修改内容。本仓库不是原作者官方发布版本，除非另有明确说明，也不代表原作者对本修改版本的认可或支持。

详细变更见 [`CHANGELOG.md`](CHANGELOG.md)，构建和贡献说明见 [`CONTRIBUTING.md`](CONTRIBUTING.md)，完整来源声明见 [`NOTICE.md`](NOTICE.md)。
