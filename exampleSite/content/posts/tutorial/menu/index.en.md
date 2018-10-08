---
title: "Hugo Content Management - Menu"
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
menu:
  main:
    parent: "posts"
    title: "how to use menus in Hugo"
    weight: 100
---

## Introduction

Menus are a powerful but simple feature for content management but can be easily manipulated in your templates to meet your design needs.

A menu is a named array of menu entries accessible by name via the `.Site.Menus.*`. Hugo support create menu for your content sections. If you want to enable this menu, just write configuration `sectionPagesMenu="main"` in your site config.

## Menu configuration


## Menu origanization

### Define your top-level menu in your site config

Example:

```
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

Menu entry's identifier is determined in the following order:

```
.Name > .LinkTitle > .Title
```

### Assign content with menu entry via Front Matter

How can we assign a piece of content with a menu? There are some example:

* add the content into a menu entry

        ```
        ---
        menu: "main"
        ---
        ```

* add the content into several menu entries

        ```
        ---
        menu: ["main", "footer"]
        ---
        ```

* build a mulit-level menu by the `parent` field

        ```
        ---
        menu:
          docs:
            parent: 'extras'
            weight: 20
        ---
        ```

## Menu template

Hugo just put all of menus and assigned content into template variable `.Site.Menus.*`. As for how to display those menu, it's depend on you. You can just use the default sections' main menu, or create your own template to show them.

### Memu template - Create a template

Example:

```
<aside>
  <ul>
    {{ $currentPage := . }}
    {{ range .Site.Menus.main }}
      {{ if .HasChildren }}
        <li class="{{ if $currentPage.HasMenuCurrent "main" . }}active{{ end }}">
          <a href="#">
            {{ .Pre }}
            <span>{{ .Name }}</span>
          </a>
          <ul class="sub-menu">
            {{ range .Children }}
              <li class="{{ if $currentPage.IsMenuCurrent "main" . }}active{{ end }}">
                <a href="{{ .URL }}">{{ .Name }}</a>
            {{ end }}
          </ul>
      {{else}}
        <li>
          <a href="{{.URL}}">
            {{ .Pre }}
            <span>{{ .Name }}</span>
          </a>
      {{end}}
    {{end}}
    <li>
      <a href="#" target="blank">Hardcoded Link 1</a>
    <li>
      <a href="#" target="blank">Hardcoded Link 2</a>
  </ul>
</aside>
```

Another Example:

```
<nav class="sidebar-nav">
  {{ range .Site.Menus.main }}
    <a href="{{ .URL }}" title="{{ .Title }}">
      {{- .Name -}}
      {{- with .Page -}}
        <span class="date">
        {{- dateFormat " (2006-01-02)" .Date -}}
        </span>
      {{- end -}}
    </a>
  {{ end }}
</nav>
```

If you want support multilingual, please use `absLangURL` or `relLangURL` instead of `absURL` and `relURL`. And you should config multilingual menu in your site config file.

### Menu template - Variable

A menu entry in a menu template has specific variables and functions to make menu management easier. Please check [here](http://gohugo.io/variables/menus/) for more information.

There is one important variable need to be detail: `.Page`:

If you use the front matter method of defining menu entries, you’ll get access to the .Page variable. This allows to use every variable that’s reachable from the page variable. In short, you can access the content page's variables via the `.Page`.

