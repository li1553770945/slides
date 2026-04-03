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

### 嵌入个人站（子页面）

产物会挂到个人站里 `public/slides/decks/<id>/` 这类子路径时，**不必**在拷贝后再去改 `index.html`、打包出来的 `index-*.js` 等文件。之前需要手改，是因为按**站点根路径**（`base: '/'`）打的包，放到子目录后资源路径会错。**只要在构建时把 `base` 设成和部署目录一致**，生成物可以直接整包丢进对应目录。

**以后每加一套幻灯片：**

1. **构建时**带上与清单里 `id` **一致**的子路径（**末尾要有 `/`**），例如：

   ```bash
   yarn build 你的文稿.md --base /slides/decks/你的id/
   ```

   等价于 `slidev build 你的文稿.md --base /slides/decks/你的id/`。

2. 把 `dist/` **整包**复制到个人站仓库，例如：

   `personal-page-fe-new/public/slides/decks/你的id/`

3. 在个人站的 `slides-manifest.json` 里加一条对应 `id` 的元数据。

`base` 会写进 HTML、JS 里的资源地址和路由前缀；与「放在个人站哪个子目录」一致后，就不需要再手改文件。

也可以在 Slidev / Vite 的配置里为某套文稿写死 `base: '/slides/decks/你的id/'`，效果与命令行 `--base` 相同。**多套幻灯片就每套各构建一次**（每套一个 `id`、一个 `base`），这是正常流程，不是额外维护负担。

个人站侧已在 `types/slides.ts` 与讲演页空状态文案（`slides.howToAdd`）里补充了上述说明，需要时可到那边对照。

若某套 deck 曾经是按根路径构建后再手改过的，**可以保留**；下次在本项目里用 `--base /slides/decks/<对应id>/` 重新 build 并覆盖拷贝后，就与以后新增的 deck 同一套流程。

## 导出 PDF（可选）

```bash
yarn export 你的文稿.md
```

需已安装 Playwright 浏览器依赖（本项目已包含 `playwright-chromium`，首次导出按 CLI 提示安装即可）。
