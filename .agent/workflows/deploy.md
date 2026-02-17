---
description: 部署博客到 GitHub Pages
---

# 部署博客工作流

## 自动部署（推荐）

推送代码到 `main` 分支后，GitHub Actions 会自动构建并部署：

```bash
cd /home/chenxq/project/githubblog && git add -A && git commit -m "更新博客" && git push origin main
```

## 手动部署（本地生成后推送）

1. 生成静态文件：

// turbo
```bash
cd /home/chenxq/project/githubblog && npx hexo clean && npx hexo generate
```

2. 确认生成的文件在 `public/` 目录中

3. 推送代码触发自动部署：

```bash
cd /home/chenxq/project/githubblog && git add -A && git commit -m "更新博客" && git push origin main
```

## 本地预览

// turbo
```bash
cd /home/chenxq/project/githubblog && npx hexo server
```

在浏览器 `http://localhost:4000` 预览效果。

## 首次部署设置

在 GitHub 上设置 Pages：

1. 进入仓库 Settings → Pages
2. Source 选择 **GitHub Actions**
3. 推送代码后 Actions 会自动运行
