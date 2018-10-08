---
title: "Hugo Content Management - Content Organization"
date: 2018-03-28T17:12:03+08:00
keywords: []
weight: 0
slug: ""
url: ""
markup: "md"
type: "posts"
isCJKLanguage: false
draft: true
tags: ["tutorial", "hugo"]
categories: ["hugo"]
series: ["hugo"]
mathjax: false
include_toc: true
include_comment: true
include_sidebar: true
---

## Introduction

Hugo assumes that the same structure that works to organize your source content is used to organize the rendered site.

## Content Organization

While Hugo supports content nested at any level, the top levels (i.e. `content/<DIRECTORIES>`) are special in Hugo and are considered the content type used to determine layouts etc. To read more about sections, including how to nest them, see [sections](https://gohugo.io/content-management/sections/).

## Map Content to URL

The following demonstrates the relationships between your content organization and the output URL structure for your Hugo website when it renders.

### URL Components

* `section`

    A default content type is determined by a piece of content’s section. section is determined by the location within the project’s content directory. section cannot be specified or overridden in front matter.

* `slug`

    A content’s slug is either name.extension or name/. The value for slug is determined by the name of the content file (e.g., lollapalooza.md) or front matter overrides.

* `path`

    A content's path is determined by the section's path to the file(does not include the slug).

* `url`

    The url is the relative URL for the piece of content. It is based on the content’s location within the directory structure or front matter overrides.



### Index/List Pages

`_index.md` has a special role in Hugo. You can keep one `_index.md` for your homepage and one in each of your content sections, taxonomies, and taxonomy terms.

Example:

content `content/posts/_index.md` will be mapped as following

```
                     url ("/posts/")
                    ⊢-^-⊣
       baseurl      section ("posts")
⊢--------^---------⊣⊢-^-⊣
        permalink
⊢----------^-------------⊣
https://example.com/posts/index.html
```

### Single Pages

Single content files in each of your sections are going to be rendered as single page templates.

Example:

content `content/posts/my-first-hugo-post.md` will be mapped as following

```
                               url ("/posts/my-first-hugo-post/")
                   ⊢------------^----------⊣
       baseurl     section     slug
⊢--------^--------⊣⊢-^--⊣⊢-------^---------⊣
                 permalink
⊢--------------------^---------------------⊣
https://example.com/posts/my-first-hugo-post/index.html
```

## Override mapping URL

There are times where you may need more control over your content. In these cases, there are fields that can be specified in the front matter to determine the destination of a specific piece of content.

The following items are defined in this order for a specific reason: items explained further down in the list will override earlier items, and not all of these items can be defined in front matter:

* `filename`

    This isn’t in the front matter, but is the actual name of the file minus the extension. For example, `/content/posts/my-first-post.md` will be rendered on `http://example.com/posts/my-first-post`.

* `slug`

    When defined in the front matter, the slug can take the place of the filename for the destination. For example, put `slug: new-post` into the front matter of `/content/posts/old-post.md`, then it'll be rendered on `http://example.com/posts/new-post/`.

* `section`

    section is determined by a content’s location on disk and cannot be specified in the front matter.

* `type`

    A content's type is also determined by its location on disk but, unlike section, it can be specified in the front matter. This can come in especially handy when you want a piece of content to render using a different layout. If you want to change page's type, just put `type: type-name` into the front matter.

* `url`

    A complete URL can be provided. This will override all the above as it pertains to the end destination. For example, put `url: /blog/new-url.md` into the front matter of `/content/posts/old-url.md`, then this page will be rendered on `https://example.com/blog/new-url/`.