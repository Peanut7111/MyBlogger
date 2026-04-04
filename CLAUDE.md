# Peanut 的冒险日志 — 项目概述

## 基本信息
- **框架**: Hugo（静态博客）
- **主题**: 自定义 Zelda（塞尔达传说）主题，无 theme 依赖
- **部署**: GitHub Pages，发布目录 `/MyBlogger/`
- **仓库**: https://github.com/Peanut7111/MyBlogger
- **工作目录**: `F:\Claude Code\Project\MyBlogger\my-blog`

## 路径与部署关键配置
- `config.yaml` 的 `baseURL: 'https://Peanut7111.github.io/MyBlogger/'`
- `publishDir: "docs"` — 构建输出到 `docs/`
- **所有模板内链接必须用 `{{ .Site.BaseURL }}` 或 `{{ "path" | relURL }}`**
  相对路径（如 `./css/zelda.css`）在子目录部署下会 404

## 模板结构
| 路径 | 用途 |
|------|------|
| `layouts/_default/single.html` | 文章页、标签页 |
| `layouts/_default/list.html` | 文章列表页 |
| `layouts/archive/list.html` | **归档页（section 索引用 list.html，非 single.html）** |
| `layouts/about/single.html` | 关于页 |
| `layouts/about/list.html` | 关于页索引 |

> **Hugo 模板规则**: section 的索引页（如 `/archive/`）使用 `list.html`，不是 `single.html`

## CSS 说明
- 主样式文件: `static/css/zelda.css`
- 背景图: `static/images/zelda-bg.jpg`
- 主题切换: `[data-theme="light/dark"]` CSS 选择器
- 主题偏好存储在 `localStorage` 的 `theme` 键

## 常用命令
```bash
git add -A
git commit -m "提交说明"
git push
# GitHub Actions 自动构建部署，约 1-2 分钟
```

## 素材参考
- [塞尔达传说：王国之泪 Wiki](https://totk.huijiwiki.com/wiki/) — 用于优化网页图标和主题素材

## 当前状态 / 未完成的事
（每次新对话先读这里，快速了解上下文）

- 归档页 Redesign 完成，年份徽章用 flex 布局（2026-04-05）
- 背景图已换成 JPG 格式
- GitHub Actions 已配置完毕，每次 push 自动部署

## 已解决的问题（避免重复踩坑）
- ❌ 不要用中文文件名做背景图（URL 编码问题）
- ❌ 不要用 `theme: ""`（会导致 module not found 错误）
- ❌ 模板内链接不要用相对路径，用 `relURL`
- ❌ 归档页不要用 `overflow: hidden`（会裁切年份徽章）
- ✅ 年份徽章用 flex 布局，不再用绝对定位
