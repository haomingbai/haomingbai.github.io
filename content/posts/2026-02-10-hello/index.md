---
title: "Hello, Hugo + Blowfish"
date: 2026-02-10
tags: ["hugo", "blowfish", "setup"]
summary: "使用 Hugo + Blowfish 搭建现代个人主页与博客的起点。"
featuredImage: "cover.png"
toc: true
---

这是一篇示例文章，用于展示 **Page Bundle**、代码高亮与图片引用。

## 代码示例（bash）

```bash
hugo new posts/2026-02-10-hello/index.md
hugo server -D
```

## 图片示例（方式 A：Markdown 引用）

![](img1.png)

## 图片示例（方式 B：figure shortcode）

{{< figure src="img1.png" alt="示例图片" caption="使用 Blowfish figure shortcode 的图片说明" >}}
