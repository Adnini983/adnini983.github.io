---
title: 撰写新文章
author: cotes
date: 2019-08-08 14:10:00 +0800
categories: [博客, 教程]
tags: [写作]
permalink: /posts/write-a-new-post/
render_with_liquid: false
---

本教程将指导你如何在 _Chirpy_ 模板中撰写一篇文章，即使你以前用过 Jekyll 也值得一读，因为许多功能需要设置特定的变量才能生效。

## 命名与路径

新建一个名为 `YYYY-MM-DD-标题.扩展名`{: .filepath} 的文件，并放入根目录的 `_posts`{: .filepath} 文件夹中。请注意，`扩展名`{: .filepath} 必须是 `md`{: .filepath} 或 `markdown`{: .filepath} 中的一种。如果你想节省创建文件的时间，可以考虑使用插件 [`Jekyll-Compose`](https://github.com/jekyll/jekyll-compose) 来完成。

## Front Matter

基本上，你需要在文章顶部按如下方式填写 [Front Matter](https://jekyllrb.com/docs/front-matter/)：

```yaml
---
title: 标题
date: YYYY-MM-DD HH:MM:SS +/-TTTT
categories: [顶级分类, 子分类]
tags: [标签]     # 标签名应始终为小写
---
```

> 文章的 _layout_ 已默认为 `post`，因此无需在 Front Matter 中添加 _layout_ 变量。
{: .prompt-tip }

### 日期时区

为准确记录文章的发布日期，你不仅需要在 `_config.yml`{: .filepath} 中设置 `timezone`，还需要在 Front Matter 的 `date` 变量中提供文章的时区。格式：`+/-TTTT`，例如 `+0800`。

### 分类与标签

每篇文章的 `categories` 最多包含两个元素，`tags` 的元素数量可以是零到无限个。例如：

```yaml
---
categories: [动物, 昆虫]
tags: [蜜蜂]
---
```

### 作者信息

文章的作者信息通常不需要填写在 _Front Matter_ 中，默认会从配置文件中的 `social.name` 变量和 `social.links` 的第一项获取。但你也可以按如下方式覆盖它：

在 `_data/authors.yml` 中添加作者信息（如果你的网站没有这个文件，请毫不犹豫地创建一个）。

```yaml
<author_id>:
  name: <全名>
  twitter: <作者的twitter>
  url: <作者的主页>
```
{: file="_data/authors.yml" }

然后使用 `author` 指定单个作者，或使用 `authors` 指定多个作者：

```yaml
---
author: <author_id>                     # 单个作者
# 或
authors: [<author1_id>, <author2_id>]   # 多个作者
---
```

也就是说，`author` 这个键也可以用来标识多个作者。

> 从文件 `_data/authors.yml`{: .filepath } 读取作者信息的好处是，页面会包含 `twitter:creator` 元标签，从而丰富 [Twitter Cards](https://developer.twitter.com/en/docs/twitter-for-websites/cards/guides/getting-started#card-and-content-attribution)，对 SEO 有好处。
{: .prompt-info }

### 文章描述

默认情况下，文章开头的文字会用于在主页的文章列表、《延伸阅读》部分以及 RSS 订阅的 XML 中显示。如果你不想显示自动生成的描述，可以使用 _Front Matter_ 中的 `description` 字段来自定义，如下所示：

```yaml
---
description: 文章的简短摘要。
---
```

此外，`description` 文本也会显示在文章页面标题的下方。

## 目录（TOC）

默认情况下，**目**录（TOC）会显示在文章的右侧面板。如果你想全局关闭它，请到 `_config.yml`{: .filepath} 中把 `toc` 变量的值设为 `false`。如果你想关闭某一篇文章的 TOC，请在文章的 [Front Matter](https://jekyllrb.com/docs/front-matter/) 中添加以下内容：

```yaml
---
toc: false
---
```

## 评论

评论的全局设置由 `_config.yml`{: .filepath} 文件中的 `comments.provider` 选项定义。一旦为该变量选择了评论系统，所有文章都会启用评论。

如果你想关闭某一篇文章的评论，请在文章的 **Front Matter** 中添加以下内容：

```yaml
---
comments: false
---
```

## 媒体资源

在 _Chirpy_ 中，我们把图片、音频和视频统称为媒体资源。

### URL 前缀

有时我们需要在一篇文章中为多个资源定义重复的 URL 前缀，这是一件很繁琐的事，你可以通过设置两个参数来避免。

- 如果你使用 CDN 来托管媒体文件，可以在 `_config.yml`{: .filepath } 中指定 `cdn`。站点头像和文章的媒体资源 URL 会加上 CDN 域名前缀。

  ```yaml
  cdn: https://cdn.com
  ```
  {: file='_config.yml' .nolineno }

- 要指定当前文章/页面的资源路径前缀，请在文章的 _front matter_ 中设置 `media_subpath`：

  ```yaml
  ---
  media_subpath: /path/to/media/
  ---
  ```
  {: .nolineno }

`site.cdn` 和 `page.media_subpath` 这两个选项可以单独使用，也可以组合使用，从而灵活地拼出最终的资源 URL：`[site.cdn/][page.media_subpath/]file.ext`

### 图片

#### 说明文字

在图片的下一行添加斜体文本，它就会成为说明文字，显示在图片底部：

```markdown
![图片描述](/path/to/image)
_图片说明_
```
{: .nolineno}

#### 尺寸

为了防止页面内容布局在图片加载时发生偏移，我们应该为每张图片设置宽度和高度。

```markdown
![桌面视图](/assets/img/sample/mockup.png){: width="700" height="400" }
```
{: .nolineno}

> 对于 SVG，你至少需要指定它的 _width_，否则它将无法被渲染。
{: .prompt-info }

从 _Chirpy v5.0.0_ 开始，`height` 和 `width` 支持缩写（`height` → `h`，`width` → `w`）。下面的示例与上面的效果相同：

```markdown
![桌面视图](/assets/img/sample/mockup.png){: w="700" h="400" }
```
{: .nolineno}

#### 位置

默认情况下，图片是居中的，但你可以使用 `normal`、`left` 和 `right` 这三个类之一来指定位置。

> 一旦指定了位置，就不应再添加图片说明文字。
{: .prompt-warning }

- **正常位置**

  在下面的示例中，图片将左对齐：

  ```markdown
  ![桌面视图](/assets/img/sample/mockup.png){: .normal }
  ```
  {: .nolineno}

- **左浮动**

  ```markdown
  ![桌面视图](/assets/img/sample/mockup.png){: .left }
  ```
  {: .nolineno}

- **右浮动**

  ```markdown
  ![桌面视图](/assets/img/sample/mockup.png){: .right }
  ```
  {: .nolineno}

#### 深色/浅色模式

你可以让图片在深色/浅色模式下跟随主题偏好。这需要你准备两张图片，一张用于深色模式，一张用于浅色模式，然后为它们指定特定的类（`dark` 或 `light`）：

```markdown
![仅浅色模式](/path/to/light-mode.png){: .light }
![仅深色模式](/path/to/dark-mode.png){: .dark }
```

#### 阴影

程序窗口的截图可以考虑显示阴影效果：

```markdown
![桌面视图](/assets/img/sample/mockup.png){: .shadow }
```
{: .nolineno}

#### 预览图

如果你想在文章顶部添加一张图片，请提供分辨率为 `1200 x 630` 的图片。请注意，如果图片的宽高比不符合 `1.91 : 1`，图片将被缩放和裁剪。

了解这些前提后，你就可以开始设置图片的属性了：

```yaml
---
image:
  path: /path/to/image
  alt: 图片替代文本
---
```

请注意，[`media_subpath`](#url-前缀) 也可以传给预览图，也就是说，当它被设置后，`path` 属性只需要填写图片文件名。

为了简单使用，你也可以直接用 `image` 来定义路径。

```yml
---
image: /path/to/image
---
```

#### LQIP

用于预览图：

```yaml
---
image:
  lqip: /path/to/lqip-file # 或 base64 URI
---
```

> 你可以在文章“[文字与排版](../text-and-typography/)”的预览图中观察到 LQIP。

用于普通图片：

```markdown
![图片描述](/path/to/image){: lqip="/path/to/lqip-file" }
```
{: .nolineno }

### 社交平台

你可以用下面的语法嵌入来自社交平台的视频/音频：

```liquid
{% include embed/{Platform}.html id='{ID}' %}
```

其中 `Platform` 是平台名称的小写形式，`ID` 是视频的 ID。

下面的表格展示了如何在给定的视频/音频 URL 中获取我们需要的两个参数，同时你也可以了解当前支持的视频平台。

| 视频 URL                                                                                                                    | 平台       | ID                       |
| -------------------------------------------------------------------------------------------------------------------------- | ---------- | :----------------------- |
| [https://www.**youtube**.com/watch?v=**H-B46URT4mg**](https://www.youtube.com/watch?v=H-B46URT4mg)                         | `youtube`  | `H-B46URT4mg`            |
| [https://www.**twitch**.tv/videos/**1634779211**](https://www.twitch.tv/videos/1634779211)                                 | `twitch`   | `1634779211`             |
| [https://www.**bilibili**.com/video/**BV1Q44y1B7Wf**](https://www.bilibili.com/video/BV1Q44y1B7Wf)                         | `bilibili` | `BV1Q44y1B7Wf`           |
| [https://www.open.**spotify**.com/track/**3OuMIIFP5TxM8tLXMWYPGV**](https://open.spotify.com/track/3OuMIIFP5TxM8tLXMWYPGV) | `spotify`  | `3OuMIIFP5TxM8tLXMWYPGV` |

Spotify 支持一些额外参数：

- `compact` - 显示精简播放器（例如 `{% include embed/spotify.html id='3OuMIIFP5TxM8tLXMWYPGV' compact=1 %}`）；
- `dark` - 强制深色主题（例如 `{% include embed/spotify.html id='3OuMIIFP5TxM8tLXMWYPGV' dark=1 %}`）。

### 视频文件

如果你想直接嵌入一个视频文件，请使用以下语法：

```liquid
{% include embed/video.html src='{URL}' %}
```

其中 `URL` 是视频文件的 URL，例如 `/path/to/sample/video.mp4`。

你还可以为嵌入的视频文件指定额外的属性。以下是允许的完整属性列表。

- `poster='/path/to/poster.png'` — 视频下载时显示的海报图
- `title='文本'` — 显示在视频下方、与图片说明文字样式相同的标题
- `autoplay=true` — 视频在可播放时自动开始播放
- `loop=true` — 播放到结尾后自动回到开头
- `muted=true` — 音频初始静音
- `types` — 用 `|` 分隔的其他视频格式扩展名。请确保这些文件与主视频文件位于同一目录。

考虑一个使用以上所有属性的示例：

```liquid
{%
  include embed/video.html
  src='/path/to/video.mp4'
  types='ogg|mov'
  poster='poster.png'
  title='演示视频'
  autoplay=true
  loop=true
  muted=true
%}
```

### 音频文件

如果你想直接嵌入一个音频文件，请使用以下语法：

```liquid
{% include embed/audio.html src='{URL}' %}
```

其中 `URL` 是音频文件的 URL，例如 `/path/to/audio.mp3`。

你还可以为嵌入的音频文件指定额外的属性。以下是允许的完整属性列表。

- `title='文本'` — 显示在音频下方、与图片说明文字样式相同的标题
- `types` — 用 `|` 分隔的其他音频格式扩展名。请确保这些文件与主音频文件位于同一目录。

考虑一个使用以上所有属性的示例：

```liquid
{%
  include embed/audio.html
  src='/path/to/audio.mp3'
  types='ogg|wav|aac'
  title='演示音频'
%}
```

## 置顶文章

你可以将一篇或多篇文章置顶到主页顶部，置顶文章会按照发布日期倒序排列。启用方法：

```yaml
---
pin: true
---
```

## 提示框

提示框有多种类型：`tip`、`info`、`warning` 和 `danger`。它们可以通过给引用块添加 `prompt-{type}` 类来生成。例如，定义一个 `info` 类型的提示框：

```md
> 提示框示例行。
{: .prompt-info }
```
{: .nolineno }

## 语法

### 行内代码

```md
`行内代码片段`
```
{: .nolineno }

### 文件路径高亮

```md
`/path/to/a/file.extend`{: .filepath}
```
{: .nolineno }

### 代码块

使用 Markdown 符号 ```` ``` ```` 可以轻松创建代码块，如下所示：

````md
```
这是一个纯文本代码片段。
```
````

#### 指定语言

使用 ```` ```{language} ```` 可以得到带语法高亮的代码块：

````markdown
```yaml
key: value
```
````

> Jekyll 标签 `{% highlight %}` 与此主题不兼容。
{: .prompt-danger }

#### 行号

默认情况下，除 `plaintext`、`console` 和 `terminal` 之外的所有语言都会显示行号。当你想隐藏某个代码块的行号时，请给它添加 `nolineno` 类：

````markdown
```shell
echo '不再显示行号！'
```
{: .nolineno }
````

#### 指定文件名

你可能已经注意到，代码语言会显示在代码块的顶部。如果你想用文件名替换它，可以添加 `file` 属性来实现：

````markdown
```shell
# 内容
```
{: file="path/to/file" }
````

#### Liquid 代码

如果你想显示 **Liquid** 片段，请将 liquid 代码用 `{% raw %}` 和 `{% endraw %}` 括起来：

````markdown
{% raw %}
```liquid
{% if product.title contains 'Pack' %}
  这个产品的标题包含单词 Pack。
{% endif %}
```
{% endraw %}
````

或者，在文章的 YAML 块中添加 `render_with_liquid: false`（需要 Jekyll 4.0 或更高版本）。

## 数学公式

我们使用 [**MathJax**][mathjax] 来渲染数学公式。出于网站性能的考虑，数学功能默认不会加载。但可以通过以下方式启用：

[mathjax]: https://www.mathjax.org/

```yaml
---
math: true
---
```

启用数学功能后，你可以使用以下语法添加数学公式：

- **块级公式** 应使用 `$$ math $$` 添加，且 `$$` 前后必须有**强制性的**空行
  - **插入公式编号** 应使用 `$$\begin{equation} math \end{equation}$$` 添加
  - **引用公式编号** 应在公式块中使用 `\label{eq:label_name}`，并在文本中内联使用 `\eqref{eq:label_name}`（见下面的示例）
- **行内公式**（在行内）应使用 `$$ math $$` 添加，且 `$$` 前后不能有空行
- **行内公式**（在列表中）应使用 `\$$ math $$` 添加

```markdown
<!-- 块级公式，保持所有空行 -->

$$
LaTeX_math_expression
$$

<!-- 公式编号，保持所有空行  -->

$$
\begin{equation}
  LaTeX_math_expression
  \label{eq:label_name}
\end{equation}
$$

可以被引用为 \eqref{eq:label_name}。

<!-- 行内公式，不能有空行 -->

"Lorem ipsum dolor sit amet, $$ LaTeX_math_expression $$ consectetur adipiscing elit."

<!-- 列表中的行内公式，转义第一个 `$` -->

1. \$$ LaTeX_math_expression $$
2. \$$ LaTeX_math_expression $$
3. \$$ LaTeX_math_expression $$
```

> 从 `v7.0.0` 开始，**MathJax** 的配置选项已移动到文件 `assets/js/data/mathjax.js`{: .filepath } 中，你可以根据需要修改选项，例如添加 [扩展][mathjax-exts]。  
> 如果你通过 `chirpy-starter` 构建网站，请将该文件从 gem 安装目录（用命令 `bundle info --path jekyll-theme-chirpy` 查看）复制到你仓库中的相同目录。
{: .prompt-tip }

[mathjax-exts]: https://docs.mathjax.org/en/latest/input/tex/extensions/index.html

## Mermaid

[**Mermaid**](https://github.com/mermaid-js/mermaid) 是一个很棒的图表生成工具。要在你的文章中启用它，请在 YAML 块中添加以下内容：

```yaml
---
mermaid: true
---
```

然后你就可以像使用其他 markdown 语言一样使用它：用 ```` ```mermaid ```` 和 ```` ``` ```` 把图表代码括起来。

## 了解更多

想了解更多关于 Jekyll 文章的知识，请访问 [Jekyll 文档：Posts](https://jekyllrb.com/docs/posts/)。
