---
title: Render Image
linktitle: "`render-image.html`"
publishdate: 2024-06-23T16:52:10+02:00
description: Render hook for markdown images
tech: [Hugo]
draft: false
---

This render hook builds off of [Hugo's built in one](https://github.com/gohugoio/hugo/blob/master/tpl/tplimpl/embedded/templates/_default/_markup/render-image.html) which allows for robust linking to page and site resources with a couple of changes:

1. Added width and height attributes to the images (this is overridden by any dimensions specified in `.Attributes`). Attributes can also be defined with a JSON object in the markdown title and if it is it will have presidence over `.Attributes`.
2. Added warnings when a referenced image isn't found in the site's assets folder.

## Source Code

{{< highlight go-html-template >}}
{{< showFile path="/layouts/_default/_markup/render-image.html" >}}
{{< /highlight >}}
