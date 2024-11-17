---
title: An ISO 8601 Date Snippet For VS Code
description: I use this to make more accurate
date: 2020-12-21T19:50:54+02:00
lastmod: 2023-04-18T19:24:04+02:00
tags: [time, snippets, vscode]
draft: false
---

I use this VS Code snippet to get granular times for my post's front matter. Note that the `+02:00` is my timezone <abbr title="South African Standard Time">SAST</abbr>—use your own [timezone](https://en.wikipedia.org/wiki/List_of_tz_database_time_zones). There's no <var class="code_var">${CURRENT_TIMEZONE}</var> unfortunately.

```json
"ISO Date": {
    "prefix": "iso8601",
    "description": "Outputs an iso8601 date (YYYY-MM-DDTHH:MM:SS+02:00)",
    "body": "${CURRENT_YEAR}-${CURRENT_MONTH}-${CURRENT_DATE}T${CURRENT_HOUR}:${CURRENT_MINUTE}:${CURRENT_SECOND}+02:00"
}
```
