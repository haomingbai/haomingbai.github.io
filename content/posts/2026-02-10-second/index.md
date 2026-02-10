---
title: "第二篇：数学公式小记"
date: 2026-02-10
tags: ["notes", "maths"]
summary: "记录Hugo博客中数学公式排版的关键点。"
featuredImage: "cover.png"
toc: true
---

{{< katex >}}

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
