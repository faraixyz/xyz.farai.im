---
title: render-link.html
linktitle: "`render-link.html`"
publishdate: 2024-06-23T16:27:21+02:00
lastmod: 2024-07-21T20:19:49+02:00
description: Render hook for markdown links
tech: [Hugo]
draft: false
---

This render hook builds off of [Hugo's built-in one](https://github.com/gohugoio/hugo/blob/master/tpl/tplimpl/embedded/templates/_default/_markup/render-link.html) and provides robust linking to pages and site assets. To this I made three changes:

1. Trimming `/content/` from the `.Destination` so I can reference files in the structure it appears in VS Code.
2. Add a warning in case a referenced page or asset doesn't exist, pointing to the offending file.
3. Added support for attributes specified as a JSON object in the markdown title.

The next thing I'm trying to do is link to non-HTML items, like the site's RSS feed.

## Source Code

{{< highlight go-html-template >}}
{{< showFile path="/layouts/_default/_markup/render-link.html" >}}
{{< /highlight >}}
