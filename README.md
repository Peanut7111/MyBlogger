# Peanut 的冒险日志

基于 Hugo 的个人博客，采用自定义塞尔达传说主题。

## 在线访问

https://Peanut7111.github.io/MyBlogger/

## 本地开发

```bash
# 启动本地预览
hugo server -D

# 构建生产版本
hugo
```

## 文章写作

文章放在 `content/posts/` 目录下，创建 `.md` 文件即可。

## 部署

push 到 GitHub 后，GitHub Actions 自动构建部署到 GitHub Pages。

## 项目结构

```
├── content/          # 文章内容
├── layouts/          # Hugo 模板
├── static/           # 静态资源（CSS、图片）
├── docs/             # 构建输出目录（GitHub Pages）
├── config.yaml       # Hugo 配置
└── CLAUDE.md         # 项目说明（供 AI 使用）
```

## 主题说明

- **浅色模式**: 白色文字 + 深色背景
- **深色模式**: 双击页面可切换
- **背景虚化**: 双击页面可开启/关闭虚化效果（50% 虚化 + 30% 亮度）

## 素材参考

- [塞尔达传说：王国之泪 Wiki](https://totk.huijiwiki.com/wiki/) — 用于优化网页图标和主题素材
