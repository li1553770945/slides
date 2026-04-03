# peacesheep 的 slides 列表

基于 [Slidev](https://sli.dev/)，入口是任意 Markdown 文件路径；不传路径时默认使用当前目录下的 `slides.md`。

## 准备

```bash
yarn install
```

## 开发（本地预览）

在仓库根目录执行，把 `你的文稿.md` 换成实际文件路径即可：

```bash
yarn dev 你的文稿.md
```

本仓库示例：

```bash
yarn dev slides/20260204组会/slides.md
```

`package.json` 里已为 dev 加上 `--open`（自动打开浏览器）和 `--bind 0.0.0.0`（局域网可访问）。需要改端口可加 `-p`，例如：`yarn dev 你的文稿.md -p 3030`。

## 构建（静态站点）

同样把入口 Markdown 写在命令后面，产物在 `dist/`：

```bash
yarn build 你的文稿.md
```

示例：

```bash
yarn build slides/20260204组会/slides.md
```

部署到子路径时需设置 base，例如：`yarn build 你的文稿.md --base /slides/20260204/`（具体以托管平台路径为准）。

## 导出 PDF（可选）

```bash
yarn export 你的文稿.md
```

需已安装 Playwright 浏览器依赖（本项目已包含 `playwright-chromium`，首次导出按 CLI 提示安装即可）。
