# blog-with-hugo

采用 Hugo 搭建的个人博客，主题选用 Stack（v3）。

## 快速开始

### 环境要求

- Hugo v0.157.0+
- Git

### 本地运行

```bash
# 克隆仓库
git clone https://github.com/swarm365/blog-with-hugo.git
cd blog-with-hugo

# 运行本地服务器
hugo server -D
```

访问 http://localhost:1313 预览博客。

### 构建生产版本

```bash
hugo --gc --minify
```

生成的静态文件位于 `public/` 目录。

## 目录结构

```
blog-with-hugo/
├── content/          # 文章内容
│   ├── post/         # 博客文章
│   ├── page/         # 独立页面（关于、归档、搜索）
│   ├── categories/   # 分类
│   └── tags/         # 标签
├── static/           # 静态资源（图片、字体等）
├── themes/           # 主题文件
├── assets/           # 资源文件（SCSS、JS 等）
├── archetypes/       # 内容模板
├── hugo.toml         # 站点配置
└── README.md         # 项目说明
```

## 内容创作

### 创建新文章

```bash
hugo new post/your-article-name.md
```

### Front Matter 格式

```markdown
---
title: "文章标题"
date: 2026-03-07
categories:
  - your-category
tags:
  - your-tag
---

文章内容...
```

## 主题配置

主题使用 Stack v3，主要配置项在 `hugo.toml`：

- `baseURL` - 站点基础 URL
- `title` - 站点标题
- `theme` - 主题名称
- `markup.goldmark.renderer.unsafe` - 启用 HTML 渲染

## 部署

### Cloudflare Pages

1. 连接 GitHub 仓库到 Cloudflare Pages
2. 构建设置：
   - **Build command**: `hugo --gc --minify`
   - **Build output directory**: `public`
3. 环境变量（如需要）：
   - `HUGO_VERSION`: `0.157.0`

### 其他平台

- **GitHub Pages**: 使用 GitHub Actions 自动部署
- **Netlify**: 自动检测 Hugo，配置构建命令
- **Vercel**: 需要配置 `vercel.json`

## 自定义

### 页脚

页脚位于 `themes/stack/layouts/partials/footer/footer.html`，包含：
- 站点名称链接
- Cloudflare 托管信息
- 外部网站链接

### 静态资源

自定义静态资源放在 `static/` 目录，如：
- `static/moe-gov.svg` - 页脚图标

## 技术栈

- **Hugo** - 静态网站生成器
- **Stack** - Hugo 主题
- **Cloudflare Pages** - 托管平台

## 许可证

GNU General Public License v3.0 (GPL-3.0)

---

> **Note**: 本文档由 AI 生成，如有问题请自行核实。
