---
title: Using iOS Shortcuts and JavaScript To Extract RSS Feed URLs From YouTube
description: Did you know YouTube have RSS feeds? Here's how I tried to get them using iOS Shortcuts
date: 2019-07-28
lastmod: 2022-10-10T12:23:06+02:00
tech: [js, apple]
draft: false
---

A few months ago, I got into RSS readers. Given how much YouTube I watch along with YouTube's broken subscription tab, I wondered if YouTube had RSS feeds. Turns out it does, but they aren't advertised. Even with an RSS reader that discovers feeds, it only works for certain pages. So I decided to use iOS Shortcuts to do it for me.

## Overview
The shortcut will works like this:
1. Parse the URL for the Channel or Playlist ID and return the feed URL
2. If step 1 works, ask the user if they want to copy the URL. If so, copy it.
3. If step 2 doesn't work, notify the user.

In this post, I'll focus on 1.

## The JavaScript
I expected to do a lot of DOM manipulation and web scraping, but the URL has everything I need.  All the feed URLs build on the URL `https://www.youtube.com/feeds/videos.xml?`.

|Type|URL Pattern|Feed URL|id|
|---|---|---|---|
|User (`user`)|`https://m.youtube.com/user/tonjesml`|`https://www.youtube.com/feeds/videos.xml?user=tonjesml`|`tonjesml`|
|Playlist (`playlist_id`)|`https://www.youtube.com/playlist&list=PLv3TTBr1W_9tppikBxAE_G6qjWdBljBHJ` or `https://www.youtube.com/watch?v=rpXGB7QQcuY&list=PLv3TTBr1W_9tppikBxAE_G6qjWdBljB`|`https://www.youtube.com/feeds/videos.xml?playlist_id=PLv3TTBr1W_9tppikBxAE_G6qjWdBljBHJ`|`PLv3TTBr1W_9tppikBxAE_G6qjWdBljBHJ`|
|Channel (`channel_id`)|`https://m.youtube.com/channel/UCU6JLYuerEUb7VrDd4zLihg`|`https://www.youtube.com/feeds/videos.xml?channel_id=UCU6JLYuerEUb7VrDd4zLihg`|`UCU6JLYuerEUb7VrDd4zLihg`|

Youtube has another URL scheme like `youtube.com/c/username` but the only way to get the RSS feed for it is to use [YouTube's API](https://developers.google.com/youtube/v3/) on the username. This is **not** the same as the `user_id`.

## The Code

Nothing too exciting although I did learn about URL parsing using `window.location` and [`URLSearchParams`](https://developer.mozilla.org/en-US/docs/Web/API/URLSearchParams).

```js
const YOUTUBE_DOMAINS = ["m.youtube.com","youtu.be", "www.youtube.com"];
const BASE_FEED_URL = "https://www.youtube.com/feeds/videos.xml?";
const pathArr = window.location.pathname.split("/");
const searchParams = new URLSearchParams(window.location.search);
const playlistID = searchParams.get("list");

if (YOUTUBE_DOMAINS.indexOf(window.location.hostname) === -1) {
    completion("Non Playlist/Channel");
}
if (playlistID){
    let playlistFeedURL = `${BASE_FEED_URL}playlist_id=${playlistID}`;
    completion(playlistFeedURL);
} else {
    let basePath = pathArr[1];
    if(basePath === "channel") {
       let channelID = pathArr[2];
       let channelFeedURL = `${BASE_FEED_URL}channel_id=${channelID}`;
       completion(channelFeedURL);
    } else if ("user" === basePath){
        let user = pathArr[2];
        let userFeedURL = `${BASE_FEED_URL}user=${user}`;
        completion(userFeedURL);
    } else {
      completion("Non Playlist/Channel");
    }
}
completion(playlistID);
```

Also note the `completion` function. This is needed to pass arguments along the shortcut.

## Conclusion

~~You can discover the full shortcut here.~~ <ins>**Note 10 October 2022: **The shortcut doesn't exist anymore and it'll be part of my project YouTube x RSS once I get around to making it again.</ins>
