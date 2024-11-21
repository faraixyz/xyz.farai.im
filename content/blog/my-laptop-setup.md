---
title: My Laptop Setup
description: Here's how I set up my laptop—software, settings and all.
tags: [pc]
publishdate: 2024-11-07T06:00:00+02:00
lastmod: 2024-11-13T20:48:00+02:00
draft: false
---

This post goes over how I set up my laptop, such as the software I use, how I configure them as well as the general settings I use on Windows. I used to have a page for my laptop's software but in case I need to reconfigure my laptop, I can always check this page out. Note that I'll try to keep this page updated as I add new software to my computer.

## General Setup

* Run updates before installing anything
* Remove Windows' annoying feature's using [Winaero Tweaker](#winaero).
* Enable Windows' Clipboard Manager with <kbd>Win</kbd> + <kbd>V</kbd>. It's lifechanging, thank me later. I just wish that iOS had one.
* Show hidden files and folders in Explorer as well as show file extensions.
* Enable a pin so that I can use Passkeys and stuff.

## Software

### Utilities

* [Winaero Tweaker](https://winaerotweaker.com/ '{"id":"winaero"}') lets me remove Window's annoying features, like:
    * Enabled classic context menus because the one in Windows 11 sucks.
* [Scoop](https://scoop.sh/) which I use to install certain packages not on WinGet, like [Dart Sass](https://sass-lang.com/) and various image codecs.
    * [vips](https://github.com/libvips/libvips) for image processing. It's supposedly faster thank Imagemagick, which is still cool. I'm also trying to add HEIF to it which is a bitch.
* [Winget Packages](https://github.com/microsoft/winget-cli) for other tools. It comes with Windows now.
    * [Hugo](https://gohugo.io/) which powers this website.
* [Chrome Remote Desktop](https://remotedesktop.google.com) for attended remote assistance.
* [Anydesk](https://anydesk.com/en) to remote to the work server since it allows unattended access.
* 
* [7-Zip](https://www.7-zip.org/) to compress/decompress files.
* [Everything](https://www.voidtools.com/) which is way better at searching for files on Windows. Sure it's because it searches filenames rather than contents but filename search is what I need to do most of the time. After installing, I enable it in the context menu. I'm trying [Everything Toolbar](https://github.com/srwi/EverythingToolbar) which [Chris Titus suggested](https://christitus.com/everything-toolbar/), but it's pretty slow right now.
* [iCloud](https://www.icloud.com/). It's pretty shit but I need it to conveniently interact with my iThings.
* [NAPS2](https://www.naps2.com/) for scanning documents.
* [PowerToys](https://learn.microsoft.com/en-us/windows/powertoys/) adds a lot of useful features to Windows, like [Awake](/the-classics/micro/power-toys-awake.md) and [Spotlight-like thing, Power Run](/the-classics/micro/launchy-power-toys.md). They're so well integrated, you don't even notice them. It warrants an entire article on it's own.
* [Google Drive](https://www.google.com/drive/) for file storage
* [KDE Connect](https://kdeconnect.kde.org/) is a cross-platform AirDrop type thing. Let's you send files and even control a computer remotley.
* [Apple Devices](https://support.apple.com/guide/devices-windows/welcome/windows) to sync my computer with my iThings. [I hate it](/the-classics/micro/apple-devices-garbage.md) though it's gotten a little better now. You can also try [CopyTrans](https://www.copytrans.net/) but it might mess with the Apple drivers since CopyTrans requires older versions of them.
* [VLC Media Player](https://www.videolan.org/vlc/) to watch videos.
* [qBittorrent](https://www.qbittorrent.org/) to download torrents. For a better experience, use [search plugins](https://github.com/qbittorrent/search-plugins) with [Jackett](https://github.com/Jackett/Jackett/releases/tag/v0.22.910).
* [yt-dlp](https://github.com/yt-dlp/yt-dlp) to download online videos.

### Productivity

* [Microsoft Office](https://www.office.com) is what I need for work. If I wasn't getting it from my mom I would use [LibreOffice](https://www.libreoffice.org) instead but what to do. [Excel is fun though](/the-classics/micro/ms-excel.md).
* [Thunderbird](https://www.thunderbird.net/) as a mail client, because Microsoft Outlook pissed me off.
* [PDF24](https://www.pdf24.org/en/) provides a lot of useful tools for working with PDFs all for free. [It works online too](https://tools.pdf24.org/en/). I should write about it someday.
* [WhatsApp](https://www.whatsapp.com/download) to receive Whatsapp chats from the work phone. For my own chats I use [Whatsapp Web](https://web.whatsapp.com)

### Programming

* [Git](https://git-scm.com/) for version control. Not very good at it but it seems to do what I want it to do right now. No particular configuration except for using my name and email.
* [VS Code](https://code.visualstudio.com) is code editor of choice. I started using it because it was way faster than Atom despite being an Electron app. I'd love to use vim but I haven't gotten around to learning it yet. I enable it with these settings:
    * enable auto-save
    * deactivate compact folders, so I can see the full folder structure in the explorer tab.
    * Add these extensions:
        * [Python](https://marketplace.visualstudio.com/items?itemName=ms-python.python), for Python development
        * [GitHub Actions](https://marketplace.visualstudio.com/items?itemName=GitHub.vscode-github-actions) to work with well...GitHub actions.
        * [gitignore](https://marketplace.visualstudio.com/items?itemName=codezombiech.gitignore) for quick access to gitignore templates.
        * [Even Better TOML](https://marketplace.visualstudio.com/items?itemName=tamasfe.even-better-toml) for [Hugo](https://gohugo.io), but I just decided to use YAML.
        * [REST Client](https://marketplace.visualstudio.com/items?itemName=humao.rest-client), to test APIs in VS Code.
* [Node.js via Fast Node Manager (fnm)](https://github.com/Schniz/fnm).
* [Python](https://www.python.org/), which was the first programming language I've ever used. I've also disabled the PATH limit if that matters for anything.
* [Notepad++](https://notepad-plus-plus.org/) for quick file editing.
* [Local](https://localwp.com/) is the recommended way to make a Local WordPress Development Environment. I've never used it but I hope to soon.
* [DevToys](https://devtoys.app/) is <q>an Open-Source Swiss Army knife for developers</q> which comes with a lot of handy tools to do things like test regular expressions, encode/decode base64 strings among other things.
* [XAAMP](https://www.apachefriends.org/) for PHP development.
* [Composer](https://getcomposer.org/) for PHP dependency manager.

### Web

* [Microsoft Edge](https://www.microsoft.com/edge/) which I'm reluctantly using after Microsoft shoved it down my face.
    * Extensions:
        * [Bitwarden](https://bitwarden.com/) is my password manager of choice. It does what it needs to do. I used to use LastPass until the new owners jacked the price up 3×, which I'm glad they did since they've [really fell off security-wise](https://arstechnica.com/information-technology/2022/12/lastpass-says-hackers-have-obtained-vault-data-and-a-wealth-of-customer-info/). I also used 1Password thanks to Canva which gave it to me for a year [after being hacked](https://www.zdnet.com/article/australian-tech-unicorn-canva-suffers-security-breach/). It was nice, but it's not worth paying for given how Bitwarden (and even Apple Passwords) is good enough and cost $0.
        * [Enhancer for YouTube](https://www.mrfdev.com/enhancer-for-youtube) which makes YouTube a lot more pleasant to use.
        * [uBlock Origin](https://github.com/gorhill/uBlock) to block ads, which are completley cancerous. Not sure how long it'll work for given how Manifest v3 is finally rolling out and [it doesn't work on Chrome anymore](https://www.theverge.com/2024/10/15/24270981/google-chrome-ublock-origin-phaseout-manifest-v3-ad-blocker), another Chromium based browser.
        * [Apple Passwords](https://support.apple.com/guide/icloud-windows/set-up-icloud-passwords-icw2babf5e03/icloud) I only have this since it was a part of the iCloud app. Doesn't work at all, like iCloud in general.
