# my_blog（Hugo + Blowfish）

这是一个基于 **Hugo extended + Blowfish** 的个人网站与博客项目，包含：主页（Profile/首页）、博客列表、文章详情、About 页面，并通过 GitHub Actions 自动部署到 GitHub Pages。

这份 README 面向后续维护者与 AI：说明仓库如何配置、如何写文章、目录结构是什么样，以及常见维护动作。

## 快速开始

1) 克隆并拉取主题（主题是 Git submodule）：

```bash
git clone --recurse-submodules <repo>
cd my_blog
```

如果已经克隆但没带 submodule：

```bash
git submodule update --init --recursive
```

2) 安装 Hugo extended

需要 Hugo **extended**（主题会用到 Hugo Pipes / SCSS / 图片处理）。

3) 本地预览：

```bash
hugo server -D
```

如端口冲突：

```bash
hugo server -D -p 1314
```

## 目录结构（重要）

Hugo 只会从特定目录参与构建，理解这些目录能减少维护困惑：

```text
.
├── hugo.toml                # 站点主配置
├── content/                 # 内容：页面与文章（Markdown）
│   ├── _index.md            # 首页内容（可选）
│   ├── about/index.md       # About 页面
│   └── posts/               # 博客文章 section
│       ├── _index.md        # 博客列表页配置
│       └── YYYY-MM-DD-slug/ # Page Bundle（文章目录）
│           ├── index.md     # 文章正文
│           ├── cover.png    # 文章封面（约定）
│           └── img*.png     # 文章内图片
├── assets/                  # Hugo Pipes 资源（会被处理/指纹化）
│   ├── avatar.png           # 作者头像（供主题读取与处理）
│   └── css/custom.css       # 自定义样式
├── static/                  # 原样拷贝到站点根目录（不经处理）
│   └── resume.pdf           # /resume.pdf（About 页面下载链接）
├── layouts/                 # 可选：覆盖/扩展主题模板（目前尽量保持为空）
├── themes/blowfish/         # Blowfish 主题（submodule）
└── .github/workflows/       # CI/CD：构建并发布到 GitHub Pages
```

注意：`public/`、`resources/`、`.hugo_build.lock` 等是构建产物/缓存，不应提交到仓库（已在 `.gitignore` 中忽略）。

## 站点配置（hugo.toml）

核心配置在 [hugo.toml](hugo.toml)：

- `theme = "blowfish"`：使用 Blowfish 主题
- `[pagination].pagerSize`：分页大小（新版本 Hugo 使用此键）
- `[params]`：主题参数
  - `customCSS = ["css/custom.css"]`：加载 [assets/css/custom.css](assets/css/custom.css)
  - `[params.author].image = "avatar.png"`：作者头像来自 [assets/avatar.png](assets/avatar.png)

## 写文章（推荐：Page Bundle）

每篇文章使用一个目录（Page Bundle），图片放同目录，路径保持相对：

```text
content/posts/2026-02-10-hello/
  index.md
  cover.png
  img1.png
```

`index.md` 头部（front matter）示例：

```yaml
---
title: "文章标题"
date: 2026-02-10
tags: ["tag1", "tag2"]
summary: "文章摘要"
featuredImage: "cover.png"
toc: true
---
```

正文中引用图片：

- Markdown：`![](img1.png)`
- Blowfish figure shortcode：

```text
{{< figure src="img1.png" alt="示例图片" caption="带说明的图片" >}}
```

## 资源放置约定

- 作者头像：放到 [assets/avatar.png](assets/avatar.png)，并在 [hugo.toml](hugo.toml) 配置 `params.author.image = "avatar.png"`。
- 简历 PDF：放到 [static/resume.pdf](static/resume.pdf)，页面访问路径为 `/resume.pdf`。

## 部署（GitHub Pages）

工作流在 [.github/workflows/deploy.yml](.github/workflows/deploy.yml)：

- 触发：push 到 `main`
- 构建：`hugo --minify --baseURL "${{ steps.pages.outputs.base_url }}/"`
- 发布：上传 `public` 作为 artifact 并部署到 Pages

如果远程构建报 “主题不兼容/函数缺失”，通常是 CI 的 Hugo 版本过旧；本仓库已将 CI 固定到兼容 Blowfish 的较新版本。

## 维护与扩展

### 更新主题（Blowfish）

```bash
git submodule update --remote --merge
```

### 清理本地构建产物

```bash
rm -rf public resources .hugo_build.lock
```

### 评论系统（可选）

Blowfish 支持多种评论系统。建议做法：

1) 在 [hugo.toml](hugo.toml) 打开对应开关（例如 `params.article.showComments` 或页面 front matter 的 `showComments`）
2) 如需自定义，按 Hugo 模板 lookup order 在 `layouts/partials/` 下新增覆盖文件（例如 `layouts/partials/comments.html`）

本仓库不再保留 “占位 comments partial”，避免误导维护者：默认完全由主题行为决定。

## 常见问题

- 主题未加载：确认已执行 `git submodule update --init --recursive`
- 图片处理报错：封面/头像请使用有效的 PNG/JPG；损坏图片会导致 Hugo `Resize/Fill` 失败
- baseURL：本地开发可用 `http://localhost:1313/`，CI 会自动注入 Pages 的 baseURL
