# 背景图片说明

## 当前背景

当前使用的是 Unsplash 上的山景图片，模拟 Link 俯瞰大陆的意境。

## 如何替换为塞尔达主题图片

1. 找一张《塞尔达传说：旷野之息》中 Link 刚苏醒时站在山上俯瞰海拉鲁大陆的图片
2. 将图片重命名为 `hyrule-bg.jpg` 或 `hyrule-bg.png`
3. 放入此文件夹（`static/images/`）

4. 然后修改 `static/css/zelda.css` 文件中的背景图片链接：

```css
/* 找到这一行 */
background-image: url('https://images.unsplash.com/photo-1519681393784-d120267933ba?w=1920&q=80');

/* 替换为本地图片 */
background-image: url('/images/hyrule-bg.jpg');
```

## 推荐图片尺寸

- 宽度：1920px 或更大
- 高度：1080px 或更大
- 格式：JPG 或 PNG

## 图片来源建议

你可以从以下渠道寻找合适的塞尔达主题图片：
- 官方截图
- 游戏壁纸网站
- 自行游戏截图
- 其他玩家的分享截图
