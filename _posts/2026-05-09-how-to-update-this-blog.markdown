---
layout: post
title: 如何更新此博客
date: 2026-05-09 14:30:00 +0800
description: 一篇指南，介绍如何给这个 Jekyll 博客发布新文章、上传图片、以及排查构建问题。
img: post-3.jpg
tags: [Blog, 教程]
author: Bai Qi
---

这个博客基于 Jekyll 搭建，托管在 GitHub Pages 上。每次提交代码后，GitHub 会自动构建并部署，一分钟内就能在 [by777.github.io](https://by777.github.io) 看到更新。

下面记录一下更新博客的完整流程。

## 创建新文章

在 GitHub 仓库中直接操作即可，不需要安装任何本地工具：

1. 打开 [github.com/by777/by777.github.io/new/master/_posts](https://github.com/by777/by777.github.io/new/master/_posts)
2. 文件名按 `年-月-日-标题.markdown` 的格式填写，例如 `2026-05-09-我的文章.markdown`
3. 粘贴下面的模板，替换标题、描述和正文内容

## 文章模板

```yaml
---
layout: post
title: 你的文章标题
date: 2026-05-09 14:30:00 +0800
description: 一句话描述这篇文章的内容
img: post-1.jpg
tags: [Blog, 生活]
author: Bai Qi
---

正文从这里开始，使用 Markdown 语法写作。

## 二级标题

这是一段文字。**加粗**，*斜体*。

![图片说明](/assets/img/你的图片.jpg)

> 引用文字

- 列表项
- 列表项
```

## YAML 注意事项

这是最容易踩坑的地方。`_config.yml` 的 YAML 格式要求**冒号后面必须有一个空格**：

```
正确: title: 我的文章
错误: title:我的文章
```

一个空格之差，整个站点构建就会失败。如果不小心改坏了 `_config.yml`，GitHub Actions 会在几十秒内报错。

## 上传图片

封面图选 `post-1.jpg` 到 `post-6.jpg`（已存在），对应不同风格：

| 图片 | 风格 |
|------|------|
| post-1.jpg | 山脉 |
| post-2.jpg | 日落 |
| post-3.jpg | 冒险 |
| post-4.jpg | 滑雪 |
| post-5.jpg | 冥想 |
| post-6.jpg | 森林 |

如果要上传新图片，打开 [github.com/by777/by777.github.io/upload/master/assets/img](https://github.com/by777/by777.github.io/upload/master/assets/img)，把图片拖进去即可。正文中引用：

```
![描述](/assets/img/你的图片.jpg)
```

## 提交与部署

在 GitHub 页面底部点击 **Commit changes**，写一句简短的提交信息，点确认。

提交后 GitHub Pages 会自动触发构建。整个过程大约一分钟。可以打开 [Actions 页面](https://github.com/by777/by777.github.io/actions) 实时查看构建状态。看到绿色的 ✓ 就说明部署成功了，刷新网站即可看到新文章。

## 排查构建失败

如果 Actions 里显示红色的 ✗，通常有两种可能：

1. **YAML 格式错误** — 检查 `_config.yml` 和你文章的 front matter，确保每个冒号后都有空格
2. **日期格式不对** — front matter 里的 `date` 必须严格遵循 `YYYY-MM-DD HH:MM:SS +0800` 格式

点进失败的 Action run，展开 "Build with Jekyll" 步骤的日志，错误信息会告诉你具体哪一行有问题。

## 其他小技巧

- **搜索功能**：网站右上角的搜索框支持全文检索
- **标签过滤**：访问 `/tags` 页面可以按标签筛选文章
- **新增独立页面**：在 `_pages/` 目录下创建文件（不是 `_posts/`）
- **不要碰 Gemfile**：这个博客不需要 Gemfile，加了反而会导致构建失败

---

博客的源码完全公开在 [github.com/by777/by777.github.io](https://github.com/by777/by777.github.io)，欢迎 Fork 和参考。
