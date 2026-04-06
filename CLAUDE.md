# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

This is a personal blog built with Hugo using the Blowfish theme. The blog content is in Chinese and is deployed to GitHub Pages via GitHub Actions.

## Development Commands

- **Start development server**: `npm run dev` (runs `hugo server --minify -D -E -F`)
- **Build for production**: `hugo --minify`
- **Update theme submodule**: `./update.sh` (updates the Blowfish theme submodule from UZPENG/blowfish)

## Architecture

### Content Structure
- `content/zh-cn/` - All blog content (Chinese)
  - `posts/` - Blog posts
  - `page/` - Standalone pages (resume, link, etc.)
- `config/_default/` - Hugo configuration files (TOML format)
  - `hugo.toml` - Main Hugo configuration
  - `params.toml` - Theme parameters (homepage layout, article settings, etc.)
  - `menus.zh-cn.toml` - Navigation menu configuration
  - `languages.zh-cn.toml` - Chinese language settings
  - `markup.toml` - Markdown renderer settings

### Theme Management
The Blowfish theme is a git submodule at `themes/blowfish` (forked from the official repo). Use `./update.sh` to update the theme.

### Deployment
GitHub Actions workflow (`.github/workflows/pages.yml`) builds the Hugo site and deploys to an external repository (`uzpeng/uzpeng.github.io`) on push to `main` branch. The workflow requires `TARGET_REPO_TOKEN` secret to be configured.

### Creating New Content
- Use Hugo archetypes: `hugo new posts/your-post.md`
- Or create markdown files manually in `content/zh-cn/posts/`
- Front matter should include at minimum: `title` and `date`
- Use `<!-- more -->` to create summary breaks for list views

### Key Configuration Details
- Base URL: `https://uzpeng.github.io/`
- Default language: `zh-cn`
- Main section for homepage: `posts`
- Goldmark renderer: `unsafe = true` (allows raw HTML)
- Theme color scheme: `slate` with light default appearance
