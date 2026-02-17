---
title: Hexo 博客部署详细教程
date: 2026-02-18 01:32:00
tags: [Hexo, GitHub Pages, 部署]
categories: [博客维护]
description: 从零开始教你如何创建 GitHub 仓库并部署 Hexo 博客。
---

# Hexo 博客部署详细教程

本教程将引导你从零开始，在 GitHub 上创建一个仓库，并将本地的 Hexo 博客部署上线。

## 1. 准备工作

确保你已经拥有一个 [GitHub 账号](https://github.com)。

## 2. 创建 GitHub 仓库

1.  登录 GitHub，点击右上角的 **+** 号，选择 **New repository**。
2.  **Repository name (仓库名)**:
    *   **推荐方案**: 使用 `<你的用户名>.github.io`。例如，如果你的用户名是 `chenxq`，仓库名填 `chenxq.github.io`。这样你的博客地址就是 `https://chenxq.github.io`，简洁好记。
    *   **备选方案**: 使用任意名称，例如 `my-blog`。这种情况下，博客地址会是 `https://<用户名>.github.io/my-blog`。**注意**: 如果选择此方案，你需要修改本地 `_config.yml` 中的 `url` 和 `root` 配置。
3.  **Public/Private**: 选择 **Public** (免费且方便)。如果你想保护源码，可以选择 Private，但 Pages 服务在免费版 Private 仓库有一些限制（通常仍可用）。建议选 **Public**。
4.  其他选项（README, .gitignore）**不要勾选**，保持仓库为空。
5.  点击 **Create repository**。

## 3. 将本地代码推送到 GitHub

回到你的本地终端（在本项目根目录），执行以下命令：

### 3.1 初始化 Git

```bash
# 如果之前没有初始化过（或者你想重新开始）
rm -rf .git # 慎用，仅在确保是新项目且无 Git 记录时使用
git init
```

### 3.2 添加远程仓库地址

将下面的 URL 替换为你刚才创建的仓库地址（在 GitHub 仓库页面可以看到，推荐使用 SSH 方式，如果配置了 SSH Key）：

```bash
# 替换 <你的用户名> 和 <仓库名>
git remote add origin git@github.com:<你的用户名>/<仓库名>.git

# 或者使用 HTTPS (需要输入密码/Token)
# git remote add origin https://github.com/<你的用户名>/<仓库名>.git
```

### 3.3 提交并推送

```bash
git add -A
git commit -m "Hexo 博客初始化"
# 推送到 main 分支
git branch -M main
git push -u origin main
```

## 4. 配置 GitHub Pages (关键步骤)

我们在项目中已经配置了 GitHub Actions 自动部署（见 `.github/workflows/deploy.yml`）。只需要在 GitHub 仓库设置中开启 Pages 功能即可。

1.  进入你的 GitHub 仓库页面。
2.  点击顶部的 **Settings** (设置)。
3.  在左侧侧边栏中找到 **Pages** (页面)。
4.  **Source (来源)**: 在 "Build and deployment" 部分，将 Source 从 "Deploy from a branch" 改为 **GitHub Actions**。
    *   *注意：我们的工作流文件会自动处理构建和上传，所以不需要选择分支。*
5.  无需其他操作，GitHub Actions 检测到代码推送后会自动运行。

## 5. 验证部署

1.  点击仓库顶部的 **Actions** 标签页。
2.  你应该能看到一个名为 "Deploy Hexo to GitHub Pages" 的工作流正在运行（黄色旋转图标）或已完成（绿色对勾）。
3.  如果显示绿色对勾，说明部署成功。
4.  在 Actions 详情页的 deploy 任务中，或者回到 **Settings -> Pages** 页面，你可以看到博客的访问链接（例如 `https://chenxq.github.io`）。
5.  点击链接访问你的博客！

## 6. 后续更新

以后每次写完文章或修改配置后，只需要执行：

```bash
git add -A
git commit -m "更新内容"
git push
```

GitHub Actions 会自动为你更新博客。

---

## 常见问题

### Q: 推送时提示 Permission denied (publickey)？
A: 说明你没有配置 SSH Key。
*   你可以改用 HTTPS 协议：`git remote set-url origin https://github.com/...`
*   或者参照 [GitHub 文档配置 SSH Key](https://docs.github.com/en/authentication/connecting-to-github-with-ssh)。

### Q: 部署成功但访问 404？
A:
1.  检查 `_config.yml` 中的 `url` 是否与实际 Pages 地址一致。
2.  如果是 `<username>.github.io` 以外的仓库名，确保 `_config.yml` 中的 `root` 设置为 `/仓库名/`。
3.  检查 Actions 日志是否有报错。

### Q: 页面样式乱了？
A: 通常是因为 `url` 或 `root` 配置不对，导致 CSS 文件加载失败。请检查 `_config.yml`。
