---
title: Things I Tried To Make My Fast Static Site Even Faster
date: 2019-01-25
lastmod: 2023-09-19T11:52:44+02:00
description: "Looking into why my site is so fast."
series: [fg-v8]
tags: [obsolete, web-perf]
draft: false
---

One thing I love about my new website is just how fast it is.

1. __I'm using a static site generator__- As great as traditional blogging solutions like WordPress are, they're slow out of the box since they have to render out each page with each request unless you do some additional configuration. Contrasted with a static site generator which builds the website up front leaving the server to just serve the web pages. They're harder to work with, but it's about right for a "techie" like me. The static site generator I use is [Hugo](https://gohugo.io) since it's really fast during development.
2. **I'm cheating**- over 90% of the data on this website is text, which takes less data than other media In two ways. It literally uses fewer data and it's easier to compress. The biggest page was 1.4MB which was because of a YouTube video. I removed the video, which cut that page's size by over 98%.
3. **I'm still cheating**- The one thing that drew me to static site generators was that I could host it for free. It started out on GitHub, but I use GitLab since it has better features. Given how big GitLab's infrastructure is, they've done all the work in making the handling of requests as fast as possible.
4. **I don't have many incentives**- I'm not a news outlet so I don't have any incentive to shove advertising and auto-playing videos into this page. This alone brings the page's size down significantly.

While it was fast and light up to this point, I wanted to see what else I could improve. So I spent a weekend trying to make the website faster and I have, at times shrinking pages to a quarter of their size.

In this article, I want to go over what worked, what didn't and the two things that made the biggest difference (gzip and minifying text) and why all my work was for nothing-ish thanks to Google Analytics.

## What Worked

### Denormalizing CSS

I used [Normalize.css](https://necolas.github.io/normalize.css/) as a reset to preserve consistency between browsers[^1]. I started by copying the file directly and including it in my project, but then I realized something. There's a whole bunch of CSS that is irrelevant to my website.

I mean, I don't have forms so there's no point in resetting the value is pointless. Removing old styles cut the number of lines by half and made the CSS about 20% lighter. It isn't much compared to later techniques, but that can grow into something meaningful. Improving things further, I overrode the default styles with my custom CSS making yet another modest change.

### Optimizing Images

I only have four images on this website, but their size still bothered me. Since they were PNGs, they were easy to optimize as I learned from reading this [post about reducing PNG file size](https://medium.com/@duhroach/reducing-png-file-size-8473480d0476). While PNGs are already compressed, you can further reduce their size by limiting the color space. Just the initial color restriction can reduce the PNG file sizes by at least 65% without a noticeable drop in quality.

## What Didn't Work

### Using a Stylesheet For Syntax Highlighting

The post [QuickPush: My First Chrome Extention](/the-classics/blog/quickpush.md) had a lot of Syntax Highlighting. So much so that it's the largest page without any images as it's more than four times the size of the average post size. Since it had two unnecessarily large code blogs, there was a lot of repetitive styling.

Since Hugo lets you generate stylesheets for syntax highlighting, I expected an increase in the CSS's page size while reducing the average page size. Turns out, the pages actually got bigger.

<div class="tround">
    <table>
        <caption>Comparison of Page Sizes Before and After Externalizing Syntax Highlighting Stylesheets (Note that links are now invalid)</caption>
        <thead>
            <th>Path</th>
            <th>Initial Size (kb)</th>
            <th>"Improved" Size (kb)</th>
            <th>% Change</th>
            </tr>
        </thead>
        <tbody>
            <tr>
                <td>/posts/quickpush/</td>
                <td>85.75</td>
                <td>93.83</td>
                <td>+9.42</td>
            </tr>
            <tr>
                <td>/posts/my-git-revisited/semester-of-java/</td>
                <td>17.86</td>
                <td>18.24</td>
                <td>+2.13</td>
            </tr>
            <tr>
                <td>/posts/my-git-revisited/qlapse/</td>
                <td>17.46</td>
                <td>18.36</td>
                <td>+5.15</td>
            </tr>
            <tr>
                <td>/posts/my-git-revisited/retweet-be-gone</td>
                <td>18.76</td>
                <td>22.77</td>
                <td>+21.40</td>
            </tr>
            <tr>
                <td>/posts/my-git-revisited/link-updater/</td>
                <td>18.76</td>
                <td>21.45</td>
                <td>+14.34</td>
            </tr>
            <tr>
                <td>/posts/senior-project/first-grep/</td>
                <td>19.94</td>
                <td>21.04</td>
                <td>+1.10</td>
            </tr>
            <tr>
                <td>/posts/hello-gitlab-pages/</td>
                <td>15.04</td>
                <td>17.69</td>
                <td>+17.62</td>
            </tr>
            <tr>
                <td>/posts/hackathonuncommon-hacks-2017/</td>
                <td>33.16</td>
                <td>33.85</td>
                <td>+2.08</td>
            </tr>
        </tbody>
        <tfoot style="font-weight:bold">
            <tr>
                <td>Total</td>
                <td>312.12</td>
                <td>341.06</td>
                <td>+9.27</td>
            </tr>
            <tr>
                <td>Average</td>
                <td>34.68</td>
                <td>37.90</td>
                <td>+9.28</td>
            </tr>
        </tfoot>
    </table>
</div>

In addition to canceling out the savings from denormalizing the CSS, it added more markup as shown in the code block before.

```html
<!-- Before -->
<pre style=color:#f8f8f2;background-color:#272822;-moz-tab-size:4;-o-tab-size:4;tab-size:4>
    ...
        <span style=color:#e6db74>&#34;AD&#34;</span>,
        <span style=color:#e6db74>&#34;AR&#34;</span>,
    ...
</pre>
<!-- After -->
<pre>
    ...
    <span class="v">&#34;AD&#34;</span><span class="p">,</span>
    <span class="v">&#34;AR&#34;</span><span class="p">,</span>
    ..
</pre>
```

Previously, the punctuation would be styled in the parent block. Externalizing the CSS, the punctuation is surrounded in a `<span>` tag with the class `p`. Repeat many times and it adds up.

### Inlining CSS

Since my CSS is very minimal, I thought it would help to inline my CSS to reduce network latency. Doing this actually made page loading slower. Looking at the network diagram, I suspect that fetching the external stylesheet is faster than it takes to parse the CSS in the head before moving onto the body.

### Switching To A Non-Tracking YouTube Embed {#yt-embed}

I was shocked to see a webpage coming in at 1.8MB. The reason it was big was that I embedded a YouTube Video which was responsible for 99% of the page's size. I suspected that by switching to the non-tracking YouTube embed with the `youtube-nocookie.com` domain, I would reduce the data transfer.

That kinda happens... by 0.03KB. Reason for that is that the non-tracking embed doesn't "phone home". As disappointing as that is, I at least know where to configure [Hugo's privacy settings](https://gohugo.io/about/hugo-and-gdpr/#all-privacy-settings).

I was still annoyed at how big this page is. After all, it was responsible for 69% of the website's total size, causing the average page size to increase by over 3 times! Because of that, I removed the embed and replaced it with a link, bringing the page's size down to 20.2KB.

## Things That Made The Biggest Difference— Compression and Minifying

I really thought that trying to find bottlenecks in my markup and CSS would make a really big difference. They only made 1% difference and that was mainly from CSS. Meanwhile, compression and minification make the biggest difference.

Hugo supports minification natively using the `--minify` flag. I don't know how smart it is (rearranging CSS to be as efficient as possible), but it's good enough. 

Compression took a bit more work. While GitLab serves compressed files, you have to compress it yourself which is easier said than done. You could just compress everything with `gzip -k .`. However, not every file will benefit from compression, like images and other binary files. Because of that, you should stick to compressing text files which are more predictable[^2].

To do that, you need to find every text file matching the pattern of text files, similar to this.

```bash
find . -regex ".*\.\(html\|css\|js\|xml\|svg\|pdf\)" -exec gzip -k9 {} +
```

This finds files in the current directory with the extensions html, css, js, xml, svg and pdf[^3] and gzips them at maximum compression, keeping the original files.

These two things made the biggest difference. All the optimizations brought down the total transfer size from 802.23KB (1414.62KB excluding the outlier) down to 479KB, a difference of 40%!(66% excluding the outlier). The average page size went from 22.28KB down to 13.16KB, a difference of 40%!

## ~~Why All This Is ~~(Slightly) Pointless~~Totally Worth It~~ Analytics Change This {#analytics}

Analytics can greatly impact site performance, so be careful when deciding to use it. Then again, those analytics can help you improve performance. Do what you want, I'm not a cop.

~~Actually, I changed my mind on February 7, 2019, so you can ignore the struck out portion. I'm disabling tracking here. I couldn't be bothered to set up tracking with your consent without being annoying like the EU tracking banners that everyone ignores. I'm probably making a big deal out of a seemingly benign issue, but this lets me focus on metrics that actually matter; thank you's, feedback and money (at some point).~~

~~When I started writing this post, I didn't include Google Analytics since I didn't know if I wanted to track or not. Now that I have it[^4], each page will get bigger by about 15KB. This makes all my optimizations slightly pointless. Keyword slightly. Reason being is that I tested all the page sizes with the cache disabled which is usually enabled. Since Google Analytics is used everywhere, it's very likely that it'll be cached. Also, you probably have an adblocker which would prevent the script from loading in the first place[^5].~~

[^1]: Doubt there's much point since there are insufficient data to see how users use my website. I agonize over but being able to use a feature not supported in IE 7, but doesn't it matter if nobody who uses IE 7 visits my site.
[^2]: I found a cool post by Julia Evans which illustrates [how gzip works](https://jvns.ca/blog/2013/10/24/day-16-gzip-plus-poetry-equals-awesome/).
[^3]: I did just say gzip doesn't work well on binary files, but the PDF in question got smaller after gzipping it.
[^4]: ~~Hopefully I'll find a non-Google Analytics suite to use instead.~~
[^5]: If you don't use an adblocker, you should start doing so. Also, if Google Analytics isn't loaded, I guess there's no point in using an adblocker to begin with? If you're worried about me tracking, enable DNT and I won't.~~Actually, no need to worry about me tracking you anymore since I'm not.~~
