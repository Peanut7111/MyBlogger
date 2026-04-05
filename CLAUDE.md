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
| `layouts/_default/single.html` | 文章页 |
| `layouts/_default/list.html` | 文章列表页、标签页 |
| `layouts/archive/list.html` | 归档页 |
| `layouts/about/list.html` | **关于页**（section 索引页，用 list.html） |
| `layouts/about/single.html` | 关于页的单个页面（几乎不用） |

> **Hugo 模板规则**:
> - **section 索引页**（如 `/about/`、`/archive/`）→ `list.html`
> - **page**（如 `/posts/my-post/`）→ `single.html`
> - 判断方法：看 `content/` 下是否有 `_index.md`，有就是 section

## 图标素材
- 图标目录: `static/icons/`
- 引用方式: `{{ "icons/文件名.webp" | relURL }}`
- 导航栏图标: `96px-Map.webp`(首页)、`96px-Ancient stone stele.webp`(文章)、`96px-Ultimate Hand.webp`(标签)、`96px-Blueprint.webp`(归档)、`96px-Character.webp`(关于)
- 三角力量: `Triforce.png`（替换 CSS 绘制的三角力量）
- 呀哈哈: `96px-korok.webp`

## 呀哈哈 Easter Egg
- 每页随机分布 4 个，隐藏在页面边角区域
- 鼠标悬停显示，移开隐藏
- 单击锁定显示，再次单击取消
- 点击后有抖动动画
- 底部提示: `每页都有4个呀哈哈！找到它们吧！`

## 三角力量传送过渡动画
- 页面加载时显示旋转三角力量 + 金色光环扩散
- 总时长约 0.5 秒
- CSS 在 `zelda.css` 底部（`.triforce-transition`）
- HTML 在 `footer.html`（`#triforceTransition`）

## CSS 说明
- 主样式文件: `static/css/zelda.css`
- 背景图: `static/images/zelda-bg.jpg`
- 主题切换: `[data-theme="light/dark"]` CSS 选择器
- 主题偏好存储在 `localStorage` 的 `theme` 键

## 常用命令
```bash
# Hugo 路径（不在 PATH 中，每次需用完整路径）
F:/Claude Code/Project/MyBlogger/tools/hugo.exe

# 本地预览（草稿可见）
F:/Claude Code/Project/MyBlogger/tools/hugo.exe server -D --baseURL "http://localhost:1313/MyBlogger/"

# Git 操作
git add -A
git commit -m "提交说明"
git push
# GitHub Actions 自动构建部署，约 1-2 分钟
```

## 工具路径
- **Hugo**: `F:/Claude Code/Project/MyBlogger/tools/hugo.exe`

## 素材参考
- [塞尔达传说：王国之泪 Wiki](https://totk.huijiwiki.com/wiki/) — 用于优化网页图标和主题素材

## 当前状态 / 未完成的事
（每次新对话先读这里，快速了解上下文）

- 导航栏图标全部替换为 `96px-*.webp` 格式（2026-04-05）
- 顶部三角力量替换为 `Triforce.png`
- 添加呀哈哈 Easter Egg（4个/页）
- 添加三角力量传送过渡动画
- 第一篇博客添加了 Triforce.png 图片
- 底部添加呀哈哈提示文字

## 已解决的问题（避免重复踩坑）
- ❌ 不要用中文文件名做背景图（URL 编码问题）
- ❌ 不要用 `theme: ""`（会导致 module not found 错误）
- ❌ 模板内链接不要用相对路径，用 `relURL`
- ❌ 归档页不要用 `overflow: hidden`（会裁切年份徽章）
- ✅ 年份徽章用 flex 布局，不再用绝对定位
- ❌ **修改模板后 Hugo Server 不生效** → 原因：Hugo preserve 从 `docs/` 读缓存 → 解决：删掉 `docs/` 重新 `hugo --cleanDestinationDir`
- ❌ **关于页模板改了不生效** → 原因：`/about/` 是 section，Hugo 用 `list.html` 不是 `single.html` → 解决：改 `layouts/about/list.html`
- ❌ **markdown 里的 H1 会和模板的 H1 重复** → 解决：在 markdown 里去掉标题，用模板提供标题和图标
- ❌ **korok zone hover 不生效** → 原因：`pointer-events: none` 阻止鼠标事件 → 解决：移除 `pointer-events: none`
- ❌ **korok zone 集中在底部** → 原因：`position: absolute` 相对于 footer 定位 → 解决：改用 `position: fixed` 并随机分布
