# 修复 GitHub Pages 部署错误 (404)

如果你收到 `Error: Failed to create deployment (status: 404)` 错误，或者部署后访问博客显示 404，通常是因为 **GitHub Pages 服务未正确开启**。

请按照以下步骤修复：

## 1. 进入仓库设置

1.  打开你的 GitHub 仓库页面：[https://github.com/Xinquan0601/chenxq.github.io](https://github.com/Xinquan0601/chenxq.github.io)
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

或者，你也可以在本地随便修改一个文件（比如给 README 加个空行）并推送，来触发新的部署：

```bash
git commit --allow-empty -m "Trigger deployment"
git push
```

## 4. 验证

等待 Actions 变成绿色对勾后，在 Pages 设置页面顶部，你应该能看到：
**"Your site is live at https://xinquan0601.github.io/chenxq.github.io/"** (或者类似的地址)。

点击该链接即可访问你的博客。

---

## 额外修复说明 (已自动处理)

我们检测到你的主题文件 (`themes/yearn`) 之前可能因为 Git 子模块 (Submodule) 问题没有被正确上传。

**我们已经自动执行了修复操作并推送到了你的仓库。**

现在你的仓库中应该包含了完整的主题代码，这能避免部署后页面样式丢失（空白页或乱码）的问题。
