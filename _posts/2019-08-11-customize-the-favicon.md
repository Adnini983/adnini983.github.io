---
title: 自定义站点图标（Favicon）
author: cotes
date: 2019-08-11 00:34:00 +0800
categories: [博客, 教程]
tags: [favicon]
permalink: /posts/customize-the-favicon/
---

[**Chirpy**](https://github.com/cotes2020/jekyll-theme-chirpy/) 的 [站点图标](https://www.favicon-generator.org/about/) 位于 `assets/img/favicons/`{: .filepath} 目录中。你可能想用自己制作的图标替换它们。下面的章节将指导你创建并替换默认的站点图标。

## 生成站点图标

准备一张尺寸为 512x512 或更大的正方形图片（PNG、JPG 或 SVG），然后访问在线工具 [**Real Favicon Generator**](https://realfavicongenerator.net/)，点击 <kbd>Pick your favicon image</kbd> 按钮上传你的图片文件。

在下一步中，网页会显示所有使用场景。你可以保留默认选项，滚动到页面底部，点击 <kbd>Next →</kbd> 按钮来生成站点图标。

## 下载并替换

下载生成的压缩包，解压后从解压出来的文件中删除以下文件：

- `site.webmanifest`{: .filepath}

然后把剩余的图片文件（`.PNG`{: .filepath}、`.ICO`{: .filepath} 和 `.SVG`{: .filepath}）复制过去，覆盖你 Jekyll 站点 `assets/img/favicons/`{: .filepath} 目录中的原始文件。如果你的 Jekyll 站点还没有这个目录，直接创建一个即可。

下表可以帮助你理解站点图标文件的变化：

| 文件 | 来自在线工具 | 来自 Chirpy |
| ------- | :--------------: | :---------: |
| `*.PNG` |        ✓         |      ✗      |
| `*.ICO` |        ✓         |      ✗      |
| `*.SVG` |        ✓         |      ✗      |


<!-- markdownlint-disable-next-line -->
>  ✓ 表示保留，✗ 表示删除。
{: .prompt-info }

下次构建站点时，站点图标将被替换为自定义版本。
