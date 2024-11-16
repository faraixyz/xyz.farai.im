---
title: breadcrumbs.html
linktitle: "`breadcrumbs.html`"
description: How I made breadcrumb navigation in Hugo
publishdate: 2022-09-03T06:00:00+02:00
lastmod: 2023-10-13T13:30:46+02:00
tech: [Hugo, HTML]
draft: false
---

Breadcrumbs are a type of navigation which shows pages in a particular order, like viewing history or, in my case, a page's hierarchy.

To make them, there's no need to over think it.

Write this where you want the breadcrumb:

```go-html-template
<p class="breadcrumbs">
	{{ partial "breadcrumbs.html" . }}
</p>
```

Then in `breadcrumbs.html`, include this:

```go-html-template{aria-label="breadcrumbs.html"}
{{ with .Parent }}
    {{ partial "breadcrumbs.html" . }}
    {{ if .Parent }}→{{ end }}
    <a href="{{ .RelPermalink }}">{{ .Title }}</a>
{{ end }}
```

It will result in something like this:

![Breadcrumbs saying Home → The Old Ones → v8 Website Redesign](/images/breadcrumb-ex.png)

The important thing is that you:
1. invoke the recursion by calling the breadcrumbs partial to the `.Parent`.
2. provide the separator (given you have one) conditional to whether the current `.Parent` has a parent and
3. link to the current crumb.

**That's it.**

You can play with semantics based on what you need. Want to use `nav > ul` instead of `p` and make them list items so you can use [Bootstrap's breadcrumbs](https://getbootstrap.com/docs/4.0/components/breadcrumb/)? Go ahead.

I spent far more time than I should have trying to solve this and this is what I ended up with. If you want the full story on how I got to this point, I might make it a premium post.
