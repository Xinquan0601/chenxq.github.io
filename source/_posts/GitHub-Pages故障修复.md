---
title: GitHub Pages 故障修复指南 (404/样式丢失)
date: 2026-02-18 01:33:00
tags: [故障排除, GitHub Pages]
categories: [博客维护]
description: 解决部署后 404 错误和样式加载失败的常见问题。
---

# 修复 GitHub Pages 部署错误 (404)

如果你收到 `Error: Failed to create deployment (status: 404)` 错误，或者部署后访问博客显示 404，通常是因为 **GitHub Pages 服务未正确开启**。

请按照以下步骤修复：

## 1. 进入仓库设置

1.  打开你的 GitHub 仓库页面。
2.  点击顶部的 **Settings** (设置) 标签页。

## 2. 配置 Pages

1.  在左侧侧边栏中，向下滚动找到 **Pages** (页面) 选项并点击。
2.  在 **Build and deployment** 部分：
    *   **Source**: 将其修改为 **GitHub Actions** (如果当前是 "Deploy from a branch")。
    *   *注意：无需选择具体的分支，Actions 会自动处理。*

## 3. 重新运行部署

配置修改后，GitHub 可能不会自动重新运行失败的 Workflow。你需要手动触发一次：

1.  点击仓库顶部的 **Actions** 标签页。
2.  在左侧找到 **Deploy Hexo to GitHub Pages**。
3.  点击最近一次失败的运行记录。
4.  点击右上角的 **Re-run jobs** -> **Re-run all jobs**。

或者，你也可以在本地随便修改一个文件（比如给 README 加个空行）并推送，来触发新的部署。

## 4. 验证

等待 Actions 变成绿色对勾后，在 Pages 设置页面顶部，你应该能看到：
**"Your site is live at ..."**。

点击该链接即可访问你的博客。

---

## 额外修复说明 (主题缺失)

如果遇到页面空白或样式完全丢失（除了 404 以外的情况），可能是主题文件丢失。

如果你使用了 `git submodule` 但配置不当，GitHub Actions 可能无法拉取主题代码。

**解决方法**：
确保 `themes/` 目录下的主题文件已包含在你的仓库中（不是作为空文件夹或 submodule 引用）。推荐做法是删除主题目录下的 `.git` 文件夹，将其作为普通代码提交。
