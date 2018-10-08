---
title: "My First Post"
featured_image: "/images/posts_section.jpg"
date: 2018-03-28T17:12:03+08:00
keywords: []
weight: 0
slug: ""
url: ""
markup: "md"
type: "posts"
isCJKLanguage: false
draft: false
tags: ["tutorial", "hugo"]
categories: ["hugo"]
series: ["hugo"]
mathjax: true
include_toc: true
include_comment: true
include_sidebar: true
---

hello world!

<!--more-->

## Enviorment Variable

`HUGO_ENV` set to `production`.

## Front Matter

### Enable MathJax

If you intend to write TeX/LaTeX/AsciiMath mathematics in the document, please put `mathjax: true` into the Front Matter.

Mathematics that is written in TeX or LaTeX format is indicated using math delimiters that surround the mathematics, telling MathJax what part of your page represents mathematics and what is normal text. The default math delimiters are `$$...$$` and `\[...\]` for displayed mathematics, and `\(...\)` for in-line mathematics.

Note in particular that the `$...$` in-line delimiters are not used by default. That is because dollar signs appear too often in non-mathematical settings, which could cause some text to be treated as mathematics unexpectedly.

If you are using MathJax within a blog, wiki, or other content management system, the markup language used by that system may interfere with the TeX notation used by MathJax. For example, if your blog uses Markdown notation for authoring your pages, the underscores used by TeX to indicate subscripts may be confused with the use of underscores by Markdown to indicate italics, and the two uses may prevent your mathematics from being displayed. See [TeX and LaTeX](https://docs.mathjax.org/en/latest/tex.html#tex-support) support for some suggestions about how to deal with the problem.

Example:

$$
\forall x \in X, \quad \exists y \leq \epsilon
$$

## Taxonomies

* Taxonomy: a categorization that can be used to classify content, e.g. "tags" is a taxonomy.
* Term: a key within the taxonomy, e.g. "machine learning" is a key of the "tags".
* Value: a piece of content assigned to a term, e.g. the article "Machine Learning Survey" is a piece of content of the "machine learning" term.

Hugo natively supports taxonomies. Without adding a single line to your site’s configuration file, Hugo will automatically create taxonomies for `tags` and `categories`.

Hugo will automatically create both a page listing all the taxonomy’s terms and individual pages with lists of content associated with each term.

## Shortcodes

### HTML Comment

You'll see nothing in the below, but you can find in HTML source.

{{< comment-html >}}
<div><a href="" title="empty url">click here</a></div>
{{< /comment-html >}}

### Markdown Comment

You'll see nothing in the below, even you go HTML source, there is nothing.

{{< comment-markdown >}}
* item1
* item2
* item3
{{< /comment-markdown >}}

## i18n

### check missing translation string

```shell
hugo --i18n-warnings | grep i18n
i18n|MISSING_TRANSLATION|en|wordCount
```

```C
#include <stdio.h>
```

{{< highlight python >}}
class someClass(object):
    def __init__(self):
        self.x = 1
{{< /highlight >}}