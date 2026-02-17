---
description: 创建新的博客文章
---

# 新建文章工作流

## 步骤

1. 创建新文章（将 `文章标题` 替换为你的标题）：

```bash
cd /home/chenxq/project/githubblog && npx hexo new "文章标题"
```

2. 用编辑器打开生成的文件（路径会在命令输出中显示），编辑 Front-matter 和正文内容：

```markdown
---
title: 文章标题
date: 2026-02-17 22:00:00
tags:
  - 标签1
  - 标签2
categories:
  - 分类名
description: 文章摘要描述
---

这里是文章摘要，会显示在首页列表中。

<!-- more -->

这里是文章正文，点击"阅读更多"后才会显示。
```

3. 本地预览（可选）：

// turbo
```bash
cd /home/chenxq/project/githubblog && npx hexo server
```

在浏览器中访问 `http://localhost:4000` 预览效果。按 `Ctrl+C` 停止预览。

4. 发布文章：

```bash
cd /home/chenxq/project/githubblog && git add -A && git commit -m "发布文章: 文章标题" && git push origin main
```

推送后 GitHub Actions 会自动构建并部署到 GitHub Pages。

## 注意事项

- **文章文件名**：建议使用英文或拼音，避免中文文件名导致的 URL 问题
- **图片资源**：将图片放在 `source/images/` 目录下，或文章同名目录下（已启用 `post_asset_folder`）
- **草稿**：使用 `npx hexo new draft "标题"` 创建草稿，发布时用 `npx hexo publish "标题"`
