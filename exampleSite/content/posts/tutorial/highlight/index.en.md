---
title: "Hugo Code Highlight"
description: ""
keywords: []
date: 2018-04-08T18:34:15+08:00
weight: 0
slug: ""
url: ""
markup: "md"
type: "posts"
isCJKLanguage: false
draft: true
categories: []
tags: []
series: []
mathjax: false
include_toc: true
include_comment: true
include_sidebar: true
---

## Introduction

From Hugo 0.28, the default syntax hightlighter in Hugo is Chroma; it is built in Go and is really, really fast – and for the most important parts compatible with Pygments.

If you want to continue to use Pygments (see below), set `pygmentsUseClassic=true` in your site config, or set it to false.

## Configuration

To make the transition from Pygments to Chroma seamless, they share a common set of configuration options.

## Usage

### Hugo Built-in Shortcode: highlight

Example:

```
{{< highlight go "linenos=table,hl_lines=8 15-17,linenostart=199" >}}
// ... code
{{< / highlight >}}
```

Shortcode Argument:

* linenos

    `linenos=inline` or `linenos=table` (table will give copy-and-paste friendly code blocks) turns on line numbers.

* hl_lines

    `hl_lines=8 15-17` lists a set of line numbers or line number ranges to be highlighted. Note that the hyphen range syntax is only supported for Chroma.

* linenostart

    `linenostart=199` starts the line number count from 199.

### Highlight in Code Fences

It is also possible to add syntax highlighting with GitHub flavored code fences. To enable this, set the pygmentsCodeFences to true.
