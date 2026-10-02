<!-- markdownlint-disable-next-line -->
<div align="center">

  <!-- markdownlint-disable-next-line -->
  # Adnini983 的博客

  一个记录 **3DS 开发机破解与自制固件** 和其它内容的中文技术博客，基于 Chirpy Jekyll 主题。

  [![GitHub license][badge-license]][license]

  [**访问站点** →][site]

</div>

## 内容

本博客的核心内容是一份完整的 **[3DS 开发机破解指南](/posts/3ds-devkit-guide/)**，涵盖：

- 通过 soundhax、MEST9、ntrboot 等方案为 3DS 开发机安装自制固件 boot9strap
- SDK 版本的降级与升级
- CTR SystemUpdater（CTR-008）刷机
- 救砖（CTRTransfer）与 NAND 数据备份
- 破解收尾：固化、安装常用自制软件

## 技术栈

本站基于 [Jekyll][jekyllrb] 生态与 [Chirpy][chirpy] 主题构建，并集成了丰富的
[第三方库][lib] 与 PWA、SEO、评论等功能。

## 部署方式

本站通过 GitHub Actions 自动构建并部署到 GitHub Pages。向 `master` 分支推送即可触发构建。

## 如何写一篇新文章

在 `_posts`{: .filepath} 目录下新建 `YYYY-MM-DD-标题.md` 文件，并按以下格式填写头部信息：

```yaml
---
title: 文章标题
date: YYYY-MM-DD HH:MM:SS +0800
categories: [分类]
tags: [标签]
author: adnini983
---
```

更多写法请参考仓库内已翻译的《[撰写新文章](/posts/write-a-new-post/)》一文。

## 致谢

本项目基于 [Jekyll][jekyllrb] 生态，并集成了 [Chirpy 主题][chirpy] 及一系列
[优秀的库][lib]。感谢所有为这些开源项目做出贡献的人！

## 许可证

本项目遵循 [MIT 许可证][license]。

[badge-license]: https://img.shields.io/github/license/cotes2020/jekyll-theme-chirpy?color=goldenrod
[license]: https://github.com/cotes2020/jekyll-theme-chirpy/blob/master/LICENSE
[site]: https://adnini983.github.io/
[jekyllrb]: https://jekyllrb.com/
[chirpy]: https://github.com/cotes2020/jekyll-theme-chirpy
[lib]: https://github.com/cotes2020/chirpy-static-assets
