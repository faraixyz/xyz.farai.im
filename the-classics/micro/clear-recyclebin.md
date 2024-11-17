---
title: How To Clean Files From A Specific Drive From Windows Recycle Bin
description: Try the Clean-RecycleBin command.
publishdate: 2024-10-21T05:15:26+02:00
tech: [windows]
tags: [snippets]
draft: false
---

I was [frantically redesigning my website yet again](/content/the-classics/blog/worry-stone.md) and like the previous times, I decided to nuke what I had worked on. This included the many files I had deleted as I was consolidating work from my previous attempts at a personal website which piled up in my Recycle Bin. I wish I could apply a filter to pick the files I wanted based on a pattern, but that isn't possible. Thankfully I set up a [Dev Drive](https://learn.microsoft.com/en-us/windows/dev-drive/) which lets me delete files from a specific drive with the [`Clear-RecycleBin`](https://learn.microsoft.com/en-us/powershell/module/microsoft.powershell.management/clear-recyclebin?view=powershell-7.4) command like so:

```ps
Clear-RecycleBin -DriveLetter X
```