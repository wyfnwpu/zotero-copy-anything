# Contributing

感谢参与 Zotero Copy Anything 的改进。

本项目源自原作者 **windfollowingheart** 的
[zotero-copy-anything](https://github.com/windfollowingheart/zotero-copy-anything)
项目。提交修改时请保留原项目来源和许可证信息。

## 开发环境

需要安装 Node.js、npm、Git 和 Zotero 10。建议使用当前仍受支持的 Node.js LTS 版本。

## 本地构建

```bash
npm install
npm run build
```

构建产物：

```text
.scaffold/build/zotero-copy-anything.xpi
```

代码格式和静态检查：

```bash
npm run lint:check
git diff --check
```

## 测试重点

每次修改菜单或启动流程后，应至少检查：

1. Zotero 能够正常加载插件，且插件设置页可打开。
2. 文献库条目右键菜单中存在 `Copy`。
3. 打开的 PDF 顶部标签页右键菜单中存在 `Copy`。
4. PDF 页面内容右键菜单中存在复制项。
5. 对应系统的辅助程序可以被下载并执行。
6. 选择本地附件后能够粘贴文件；未下载到本地的附件应给出失败提示。

## 提交修改

- 保留 `LICENSE`、原作者署名和原项目链接。
- 在 README 和变更记录中明确说明本仓库源自原作者项目以及新增修改。
- 不得将本修改版本描述为原作者官方版本，也不得暗示原作者为本版本背书。
- 修改版本号后同步更新 `package-lock.json`。
- 修改后运行构建、格式检查和 `git diff --check`。
- 不要提交 `node_modules`、本地 Zotero 数据目录或调试日志。

## 许可证

本项目及其修改版本遵循 [AGPL-3.0-or-later](LICENSE)。提交代码即表示你有权在该许可证下贡献这些内容。
