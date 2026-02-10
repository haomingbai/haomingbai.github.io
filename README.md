# Hugo + Blowfish 现代个人主页与博客

这是一个基于 **Hugo extended + Blowfish** 的个人主页与博客模板，兼顾现代视觉与移动端体验。只需 `git push` 到 `main`，GitHub Actions 会自动部署到 GitHub Pages。

## 站点用途与技术栈

- 生成器：Hugo **extended**
- 主题：Blowfish
- 目标：个人主页 + 博客，两者均衡，移动端友好

## 写文章流程（Page Bundle）

1) 新建文章目录（Page Bundle）：

```
content/posts/2026-02-10-hello/
  index.md
  cover.png
  img1.png
```

2) `index.md` front matter 模板：

```
---
title: "文章标题"
date: 2026-02-10
tags: ["tag1", "tag2"]
summary: "文章摘要"
featuredImage: "cover.png"
toc: true
---
```

3) 图片放在同目录，并用两种方式引用：

- Markdown 直接引用：`![](img1.png)`
- Blowfish `figure` shortcode：

```
{{< figure src="img1.png" alt="示例图片" caption="带说明的图片" >}}
```

> 约定：封面图片使用 `cover.png`。

## 本地预览（可选但推荐）

1) 安装 Hugo extended：

- macOS: `brew install hugo`
- Windows: `scoop install hugo-extended`
- Linux: 建议从 GitHub Releases 下载 extended 版本

2) 克隆仓库并拉取子模块：

```
git clone --recurse-submodules <your-repo>
```

3) 启动本地服务：

```
hugo server -D
```

常见问题：

- **主题未加载**：确认子模块已拉取（`--recurse-submodules`）。
- **端口冲突**：使用 `hugo server -D -p 1314`。
- **图片不显示**：确认图片放在文章同目录，并使用相对路径。

## 部署说明（GitHub Actions）

- push 到 `main` → Actions 自动构建并部署到 GitHub Pages。
- 仓库 Settings → Pages 选择 **GitHub Actions** 作为部署方式（如未默认选择）。
- **Project Pages / User Pages**：CI 使用 `actions/configure-pages` 的 `base_url` 输出注入 `--baseURL`，无需手动改 `baseURL`。

## 未来扩展评论区（giscus）

- 入口文件：`layouts/partials/comments.html`
- 开关位置：`hugo.toml` 中的 `[params.comments]`（将 `enabled = true`）
- 接入步骤概览：
  1. 在 GitHub 仓库开启 Discussions
  2. 用 giscus 配置向导生成配置
  3. 将生成的 script 放入 `layouts/partials/comments.html`
