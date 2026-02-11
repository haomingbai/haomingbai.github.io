---
title: "Hello, Hugo + Blowfish"
date: 2026-02-10
tags: ["hugo", "blowfish", "setup"]
summary: "使用 Hugo + Blowfish 搭建现代个人主页与博客的起点。"
featuredImage: "cover.png"
toc: true
---

{{< katex >}}

这是一篇示例文章，用于展示 **Page Bundle**、代码高亮与图片引用。

## 代码示例（bash）

```bash
hugo new posts/2026-02-10-hello/index.md
hugo server -D
```

## 图片示例（方式 A：Markdown 引用）

![Image 1](img1.png)

## 图片示例（方式 B：figure shortcode）

{{< figure src="img1.png" alt="示例图片" caption="使用 Blowfish figure shortcode 的图片说明" >}}

## 数学公式（行内）

这是一个数学公式，表达一个简单的线性方程：$x+y=1$。

## 数学公式（公式块）

$$
\begin{cases}
  x_1 + x_2 + x_3 = 1 \\\
  x_1 + 2x_2 + x_3 = 3 \\\
  x_1 + x_2 + 2x_3 = 4
\end{cases}
$$

然后是一个简单的矩阵：

$$
\begin{bmatrix}
  1 & 2 & 3 \\\
  4 & 5 & 6 \\\
  7 & 8 & 9
\end{bmatrix}
$$

注意，在Hugo中，公式换行需要三个斜杠。
