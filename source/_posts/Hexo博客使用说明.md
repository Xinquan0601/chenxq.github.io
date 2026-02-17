---
title: Hexo 博客项目使用说明书
date: 2026-02-18 01:31:00
tags: [Hexo, 教程]
categories: [博客维护]
description: 详细介绍了本博客项目的使用、配置和维护方法。
---

# Hexo 博客项目使用说明书

本文档详细介绍了如何使用、配置和维护本 Hexo 博客项目。

## 目录

1. [快速开始](#快速开始)
2. [常用命令](#常用命令)
3. [项目配置](#项目配置)
4. [主题配置 (Yearn)](#主题配置-yearn)
5. [常见问题](#常见问题)

---

## 快速开始

### 1. 环境准备

确保本机已安装 Node.js (推荐 v18+) 和 Git。

### 2. 安装依赖

首次克隆项目后，请在项目根目录运行：

```bash
npm install
```

---

## 常用命令

### 新建文章

使用以下命令快速创建新文章：

```bash
# 格式: npx hexo new "文章标题"
npx hexo new "我的第一篇文章"
```

生成的文章文件位于 `source/_posts/我的第一篇文章.md`。

### 本地预览

启动本地服务器预览博客效果：

```bash
npx hexo server
```

访问地址: [http://localhost:4000](http://localhost:4000)

**注意**: 如果提示端口被占用，请参考 [常见问题](#常见问题)。

### 部署博客

推荐使用 Git 推送触发自动部署：

```bash
git add -A
git commit -m "更新博客文章"
git push origin main
```

稍等片刻，GitHub Actions 会自动构建并部署到 GitHub Pages。

👉 **详细步骤请参考**: [Hexo 博客部署详细教程](/2026/02/18/Hexo部署指南/)

---

## 项目配置

站点主配置文件位于 `_config.yml`。

### 关键配置项

*   **title**: 博客标题
*   **author**: 作者名称
*   **url**: 你的 GitHub Pages 地址 (例如 `https://username.github.io`)
*   **language**: 语言设置 (默认 `zh-CN`)
*   **theme**: 主题设置 (当前为 `yearn`)

---

## 主题配置 (Yearn)

Yearn 主题的配置文件位于 `themes/yearn/_config.yml`。

### 常用修改

*   **menu**: 顶部导航菜单
*   **subnav**: 社交链接配置 (GitHub, Email 等)
*   **avatar**: 头像 URL (可以是本地路径 `/images/avatar.jpg` 或网络图片)
*   **leftBackground**: 首页左侧背景图列表 (每次刷新随机显示)

### 修改头像

1. 将头像图片放入 `source/images/` 目录（例如 `avatar.jpg`）
2. 修改 `themes/yearn/_config.yml`:
    ```yaml
    avatar: /images/avatar.jpg
    ```

---

## 常见问题

### 1. 端口被占用 (EADDRINUSE: :::4000)

如果运行 `npx hexo server` 时提示 `FATAL Port 4000 has been used`，说明之前的服务没有正常关闭。

**解决方法**:

1. **查找占用进程**:
    ```bash
    lsof -i :4000
    ```
2. **终止进程**:
    ```bash
    kill <PID>
    # 或者一键杀掉所有 hexo 进程
    pkill -f hexo
    ```
3. **更换端口启动**:
    ```bash
    npx hexo server -p 4001
    ```

### 2. 部署失败

请检查 GitHub Actions 页面查看构建日志。常见原因：
*   文章 Front-matter 格式错误
*   缺少必要的插件依赖 (尝试运行 `npm install` 修复)
*   **Pages 服务未开启 (404 错误)**: 请参考 [修复 GitHub Pages 部署错误](/2026/02/18/GitHub-Pages故障修复/)
*   **样式错乱 (CSS 加载失败)**: 你的博客部署在子路径 (例如 `/chenxq.github.io/`)，请检查 `_config.yml` 中的 `url` 和 `root` 配置是否包含了该子路径。
