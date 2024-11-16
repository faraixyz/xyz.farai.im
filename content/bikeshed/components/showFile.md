---
title: showFile.html Shortcode
linktitle: "`showFile.html` Shortcode"
description: A "meta" shortcode which I use to show the contents of a specific file I use on this site and applies syntax highlighting to it.
publishdate: 2023-07-21T22:58:03+02:00
lastmod: 2024-06-23T16:28:17+02:00
tech: [Hugo]
draft: false
---

A "meta" shortcode which I use to show the contents of a specific file I use on this site and applies syntax highlighting to it. For some reason I can't use syntax highlighting via code fences in markdown so you'll need to use the [highlight shortcode](https://gohugo.io/content-management/syntax-highlighting/).

## Arguments

```go-html-template
{{</* showFile path="" lang="" */>}}
```

* `path` is the file you want to show (from project root including mounts)
* `lang` is the file type. By default it is inferred by the file extension.

## Source Code

Very meta.

{{< highlight go-html-template >}}
{{< showFile path="/layouts/shortcodes/showFile.html" >}}
{{< / highlight >}}
