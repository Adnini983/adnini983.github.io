---
title: 快速开始
description: >-
  通过这份全面的概览来开始了解 Chirpy 的基础知识。
  你将学习如何安装、配置和使用你的第一个基于 Chirpy 的网站，以及如何将它部署到服务器上。
author: cotes
date: 2019-08-09 20:55:00 +0800
categories: [博客, 教程]
tags: [快速开始]
permalink: /posts/getting-started/
---

## 创建站点仓库

在创建你的站点仓库时，根据你的需求有两种选择：

### 方式一：使用 Starter（推荐）

这种方法可以简化升级、隔离不必要的文件，非常适合希望把精力集中在写作上、只需最少配置的用户。

1. 登录 GitHub，进入 [**starter**][starter]。
2. 点击 <kbd>Use this template</kbd>（使用此模板）按钮，然后选择 <kbd>Create a new repository</kbd>（创建新仓库）。
3. 将新仓库命名为 `<username>.github.io`，把 `username` 替换为你小写的 GitHub 用户名。

### 方式二：Fork 主题

这种方法便于修改功能或 UI 设计，但在升级时会带来挑战。所以除非你熟悉 Jekyll 并打算大幅修改这个主题，否则不要尝试。

1. 登录 GitHub。
2. [Fork 主题仓库](https://github.com/cotes2020/jekyll-theme-chirpy/fork)。
3. 将新仓库命名为 `<username>.github.io`，把 `username` 替换为你小写的 GitHub 用户名。

## 配置开发环境

创建好仓库后，就该配置你的开发环境了。主要有两种方法：

### 使用 Dev Containers（Windows 推荐）

Dev Containers 使用 Docker 提供一个隔离的环境，可以防止与你的系统冲突，并确保所有依赖都在容器内被管理。

**步骤**：

1. 安装 Docker：
   - 在 Windows/macOS 上，安装 [Docker Desktop][docker-desktop]。
   - 在 Linux 上，安装 [Docker Engine][docker-engine]。
2. 安装 [VS Code][vscode] 和 [Dev Containers 扩展][dev-containers]。
3. 克隆你的仓库：
   - 对于 Docker Desktop：启动 VS Code，然后[在容器卷中克隆你的仓库][dc-clone-in-vol]。
   - 对于 Docker Engine：先在本地克隆你的仓库，然后通过 VS Code [在容器中打开它][dc-open-in-container]。
4. 等待 Dev Containers 配置完成。

### 本地配置（类 Unix 系统推荐）

对于类 Unix 系统，你可以本地配置环境以获得最佳性能，当然也可以改用 Dev Containers。

**步骤**：

1. 按照 [Jekyll 安装指南](https://jekyllrb.com/docs/installation/) 安装 Jekyll，并确保已安装 [Git](https://git-scm.com/)。
2. 将你的仓库克隆到本地机器。
3. 如果你 Fork 了主题，请安装 [Node.js][nodejs]，并在根目录运行 `bash tools/init.sh` 来初始化仓库。
4. 在仓库根目录运行命令 `bundle install` 来安装依赖。

## 使用方法

### 启动 Jekyll 服务器

要在本地运行站点，请使用以下命令：

```terminal
$ bundle exec jekyll serve
```

> 如果你使用的是 Dev Containers，你必须在 **VS Code** 的终端中运行该命令。
{: .prompt-info }

几秒钟后，本地服务器就可以在 <http://127.0.0.1:4000> 访问了。

### 配置

根据需要更新 `_config.yml`{: .filepath} 中的变量。一些常见的选项包括：

- `url`
- `avatar`
- `timezone`
- `lang`

### 社交联系方式

社交联系方式显示在侧边栏底部。你可以在 `_data/contact.yml`{: .filepath} 文件中启用或禁用特定的联系方式。

### 自定义样式表

要自定义样式表，请将主题的 `assets/css/jekyll-theme-chirpy.scss`{: .filepath} 文件复制到你 Jekyll 站点的相同路径，然后在文件末尾添加你的自定义样式。

### 自定义静态资源

静态资源配置是在 `5.1.0` 版本中引入的。静态资源的 CDN 定义在 `_data/origin/cors.yml`{: .filepath } 中。你可以根据网站发布地区的网络状况替换其中的一些资源。

如果你更愿意自托管静态资源，请参考 [_chirpy-static-assets_](https://github.com/cotes2020/chirpy-static-assets#readme) 仓库。

## 部署

在部署之前，请检查 `_config.yml`{: .filepath} 文件，确保 `url` 配置正确。如果你更喜欢[**项目站点**](https://help.github.com/en/github/working-with-github-pages/about-github-pages#types-of-github-pages-sites)而不使用自定义域名，或者你想在 GitHub Pages 之外的服务器上通过基础 URL 访问你的网站，请记得把 `baseurl` 设置为你的项目名，并以斜杠开头，例如 `/project-name`。

现在你可以选择下面的 _一种_ 方法来部署你的 Jekyll 站点。

### 使用 GitHub Actions 部署

请准备以下事项：

- 如果你使用的是 GitHub 免费套餐，请保持你的站点仓库为公开状态。
- 如果你已经把 `Gemfile.lock`{: .filepath } 提交到仓库，而你的本地机器不是 Linux，请更新锁定文件的平台列表：

  ```console
  $ bundle lock --add-platform x86_64-linux
  ```

接下来，配置 _Pages_ 服务：

1. 进入你 GitHub 上的仓库。选择 _Settings_（设置）选项卡，然后在左侧导航栏中点击 _Pages_。在 **Source**（来源）部分（位于 _Build and deployment_ 构建和部署下），从下拉菜单中选择 [**GitHub Actions**][pages-workflow-src]。

2. 向 GitHub 推送任意提交以触发 _Actions_ 工作流。在你仓库的 _Actions_（操作）选项卡中，你应该能看到 _Build and Deploy_（构建与部署）工作流正在运行。一旦构建完成并成功，站点将自动部署。

你现在可以访问 GitHub 提供的 URL 来访问你的站点。

### 手动构建与部署

对于自托管服务器，你需要在本地构建站点，然后把站点文件上传到服务器。

进入源项目的根目录，用以下命令构建你的站点：

```console
$ JEKYLL_ENV=production bundle exec jekyll b
```

除非你指定了输出路径，否则生成的站点文件会放在项目根目录的 `_site`{: .filepath } 文件夹中。将这些文件上传到你的目标服务器。

[nodejs]: https://nodejs.org/
[starter]: https://github.com/cotes2020/chirpy-starter
[pages-workflow-src]: https://docs.github.com/en/pages/getting-started-with-github-pages/configuring-a-publishing-source-for-your-github-pages-site#publishing-with-a-custom-github-actions-workflow
[docker-desktop]: https://www.docker.com/products/docker-desktop/
[docker-engine]: https://docs.docker.com/engine/install/
[vscode]: https://code.visualstudio.com/
[dev-containers]: https://marketplace.visualstudio.com/items?itemName=ms-vscode-remote.remote-containers
[dc-clone-in-vol]: https://code.visualstudio.com/docs/devcontainers/containers#_quick-start-open-a-git-repository-or-github-pr-in-an-isolated-container-volume
[dc-open-in-container]: https://code.visualstudio.com/docs/devcontainers/containers#_quick-start-open-an-existing-folder-in-a-container
