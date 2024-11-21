---
title: lite-yt.html
description: A better YouTube embed for Hugo
publishdate: 2024-11-10T05:58:00+02:00
linktitle: "`lite-yt.html`"
tags: [web-perf, youtube]
tech: [Hugo, JS]
draft: false
---

I've wanted to embed YouTube videos to my site for a while now, but I was always too scared to do it. Also, it came with a lot of performance issues that I thought were so bad [I removed it](/the-classics/blog/making-site-faster.md#yt-embed). Well, there's a lot of YouTube videos I'd like to include on this site and I've also found a way to do it performantly.

With the help of [Paul Irish's Lite YouTube Embed](https://github.com/paulirish/lite-youtube-embed?tab=readme-ov-file) implementation, I've made the `lite-yt.html` shortcode to improve web performance by loading the video only when requested. This makes a page load 0.4s with 117KB vs 3.5s with 3.9MB—6× faster using 3% of the data[^1]. It's also progressivley enhanced so it'll work in RSS just fine. It still needs a bit of tidying up but it should be good for now. Once you're done with this, see my first post using this shortcode.

## Usage and Example

First you'll need to include the partial `lite-yt.html` in your header so that the embed's scripts only load when the lite-yt shortcode is detected.

```go-html-template
{{ partial "lite-yt.html" . }}
```

Then you make a partial like this:

```go-html-template
{{</* lite-yt id="" title="" params="" ytapi="" */>}}
```

* `id` is the id of the video—the `v` parameter. So for the video `https://www.youtube.com/watch?v=dQw4w9WgXcQ`, the id will be `dQw4w9WgXcQ`
* `title` is the name of the video.
* `params` is the param string containing any [embed settings](https://developers.google.com/youtube/player_parameters#Parameters) you would like to have.
* `ytapi` should be specified if you want to [use the YouTube Player API](https://developers.google.com/youtube/player_parameters#Parameters).

Here's an example using [this cool video](https://www.youtube.com/watch?v=dQw4w9WgXcQ):

{{< lite-yt id="dQw4w9WgXcQ" title="Rick Astley - Never Gonna Give You Up (Official Music Video)" >}}

## Source Code

### `partials/lite-yt.html`

{{< highlight go-html-template >}}
{{< showFile path="/layouts/partials/lite-yt.html" >}}
{{< / highlight >}}

### `shortcodes/lite-yt.html`

{{< highlight go-html-template >}}
{{< showFile path="/layouts/shortcodes/lite-yt.html" >}}
{{< / highlight >}}

[^1]: Yeah so that includes the live reload script on the test server which is like 80KB, so it performs even better. Just see [Paul's comparison instead](https://github.com/paulirish/lite-youtube-embed?tab=readme-ov-file#comparison)
