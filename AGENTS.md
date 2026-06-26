# AGENTS.md

## 命令

- **开发服务器**: `npm run dev` — 运行 `hugo server --minify -D -E -F`（启用草稿、未来日期、过期内容）
- **生产构建**: `hugo --minify`
- **更新主题子模块**: `./update.sh` — 从 `UZPENG/blowfish` 拉取最新版本，提交并推送

无 lint、typecheck 或测试命令，这是纯 Hugo 内容站点。

## 核心架构

- **主题**: Blowfish，作为 git 子模块安装在 `themes/blowfish`，指向 fork 仓库（`UZPENG/blowfish`）。克隆时需使用 `--recursive` 或执行 `git submodule update --init --recursive`。
- **配置**: TOML 格式，位于 `config/_default/`。主配置文件为 `hugo.toml`。
- **内容语言**: 中文（`zh-cn`），所有内容位于 `content/zh-cn/` 下。
  - `posts/` — 博客文章
  - `page/` — 独立页面（简历、链接等）

## 内容创建

- 新文章放在 `content/zh-cn/posts/`。Front matter 至少需要 `title` 和 `date`。
- `summaryLength = 0` — Hugo 不会自动截断摘要，需使用 `<!-- more -->` 标记列表页摘要分隔。
- Goldmark 渲染器允许原始 HTML（`unsafe = true`）。

## 部署

- 推送到 `main` 分支会触发 GitHub Actions（`.github/workflows/pages.yml`）。
- 构建产物部署到外部仓库 `uzpeng/uzpeng.github.io` 的 `master` 分支。
- 需要在 GitHub 仓库设置中配置 `TARGET_REPO_TOKEN` 密钥。
