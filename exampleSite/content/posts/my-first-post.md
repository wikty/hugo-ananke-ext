---
title: "我的第一篇文章"
featured_image: "/images/posts_section.jpg"
date: 2018-03-28T17:12:03+08:00
keywords: []
weight: 0
slug: ""
url: ""
markup: "md"
type: "posts"
isCJKLanguage: true
draft: false
tags: ["tutorial", "hugo"]
categories: ["hugo"]
series: ["hugo"]
mathjax: true
include_toc: true
include_comment: true
include_sidebar: true
---

你好，世界！

<!--more-->

## 环境变量

在最终发布网站时，应该在托管的主机上设置环境变量 `HUGO_ENV="production"`。这样可以让 Hugo 根据不同环境生成不同的网站内容。

## Front Matter：文档头

### 开启支持 MathJax

如果打算在文档中编写 TeX/LaTeX/AsciiMath 数学公式，则需要在该文档的 Front Matter 中填写字段 `mathjax: true`。按需开启 MathJax，可以加快某些页面的加载速度。

文档中以 TeX/LaTeX 格式编写的数学公式，应该用定界符跟文档其它内容隔开。根据数学公式是区块的，还是行内的，定界符也分别对应两种：`$$...$$` 和 `\[...\]` 用于区块公式；`\(...\)` 用于行内公式。注：由于 `$` 会经常出现在英语文档中，所以为了避免解析歧义，默认是不支持 `$...$` 行内定界符的。

TeX/LaTeX 数学公式语法跟 Markdown 等语言语法解析可能会引起歧义。以 Markdown 中的下划线表示斜体语法为例，同样下划线在 TeX/LaTeX 中却有不同的语义，因此会引起解析歧义。解决方案参见[此处](https://docs.mathjax.org/en/latest/tex.html#tex-support)。

TeX/LaTeX 数学公式语法样例：

$$
\forall x \in X, \quad \exists y \leq \epsilon
$$

## Taxonomies：内容分类

* Taxonomy： 表示一个对内容进行分类的规则，比如 "tags" 和 "categories" 就是 Hugo 内置的两个分类规则。
* Term： 表示分类规则中的一个键，比如 "machine learning" 就是隶属于 "categories" 的一个键。
* Value： 表示跟分类规则中某个键所关联的内容，比如 "Machine Learning: A Review" 这篇文章就是跟键 "machine learning" 关联的内容。

Hugo 会为每个 Taxonomy 创建一个页面来列出属于它的所有 Term，并且会为每个 Term 创建一个页面来列出跟它关联的所有文章。

## Menu：内容组织

将内容按照菜单的层级结构来组织。

可以将同一个文档添加到不同菜单中；菜单支持任意深度的嵌套；

A menu is a named array of menu entries accessible by name via the .Site.Menus site variable.

Hugo 默认菜单项 .Site.Menus.main。

菜单支持多语言。

菜单的变量：

* url
* name
* identifier
* pre
* post
* weight
* parent
* children

将配置信息关联到菜单，在 `config.toml` 中

```toml
[[menu.main]]
    name = "about hugo"
    pre = "<i class='fa fa-heart'></i>"
    weight = -110
    identifier = "about"
    url = "/about/"
[[menu.main]]
    name = "getting started"
    pre = "<i class='fa fa-road'></i>"
    weight = -100
    url = "/getting-started/"
```

将文档关联到菜单：

通过 Front Matter 来将文档关联到菜单

* 添加到一个菜单

    ```yaml
    menu: "main"
    ```

* 添加到多个菜单

    ```yaml
    menu: ["main", "footer"]
    ```

* 添加到菜单并提供参数

    ```yaml
    menu: 
      docs:
        title: "how to use menus in templates"
        parent: "templates"
        weight: 20
    ```

注：菜单嵌套通过字段 `parent` 来实现，`parent` 指向另一个父级菜单项。

总之，一般顶级菜单项通过配置文件指定，然后在 Front Matter 中通过 `parent` 来创建菜单层级结构。






## Shortcodes：增强 Markdown 的表达能力

### HTML 注释

下面的内容不会出现，但会出现在 HTML 源代码中。

{{< comment-html >}}
<div><a href="" title="empty url">click here</a></div>
{{< /comment-html >}}

### Markdown 注释

下面的内容不会出现，也不会出现在 HTML 源码中。

{{< comment-markdown >}}
* item1
* item2
* item3
{{< /comment-markdown >}}

## i18n：多语言支持

### translation key

一个 translation key 指代一个抽象概念，可以对应多个语言中的不同翻译和解释。

多语言对某个 translation key 的定义，保存在 `i18n/` 目录中相应以语言代码命名的文件中，比如：`zh-cn.toml`，该文件内容样例如下：

```toml
[translations]
other = "翻译"

[wordCount]
other = "这篇文章有 {{ .WordCount }} 个字"

[readingTime]
one = "大概需要阅读一分钟"
other = "大概需要阅读 {{.Count}} 分钟"
```

要使用该 translation key，在模板文件中使用 `{{ i18n "translation_id" }}` 或 `{{ T "translation_id" }}` 语法

要查看有哪些 translation key 是遗漏定义的：

```shell
hugo --i18n-warnings | grep i18n
i18n|MISSING_TRANSLATION|en|wordCount
```

建议不要手动编辑 translation key 定义文件，应该使用 [goi18n](https://github.com/nicksnyder/go-i18n)来对其管理。