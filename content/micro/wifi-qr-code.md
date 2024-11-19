---
title: How To Make A WiFi QR Code
publishdate: 2024-11-04T05:58:00+02:00
description: I'm ashamed to say it took me this lon
tags: [networking, qr]
draft: false
---

*I forgot to publish this a couple weeks ago, lol 🥲*.
___

Ashamed this took me longer to figure out than it should but to make a QR code do that someone can connect to a WiFi network it needs this text:

```txt
WIFI:T:WPA;S:<ssid>;P:<password>;;
```

where `<ssid>` is the router's broadcase name (ssid) and `<password>` is well... the network password.

That should do for the most part but there are some other parameters you can add which you can get from the [ZXing wiki](https://github.com/zxing/zxing/wiki/Barcode-Contents#wi-fi-network-config-android-ios-11).

I tried to figure this stuff out using [WPA 3.3 Spec [PDF: 520KB]](https://www.wi-fi.org/system/files/WPA3%20Specification%20v3.3.pdf) and [Anthropic's Claude LLM](https://claude.ai/) and explain the advanced options but the ZXing wiki is better at it than me.
___

Know what? I've been doing a lot of things with QR codes lately and one thing that's really annoying is that a lot of QR code generators are constantly trying to upsell you. This nonsense is making me want to make my own no-nonsense QR code generator, like [the one by the Disenshittify Project](https://deshittify.us/qr-coder/index.html). Given that I've decided to make [my own QR Code generator](https://faraixyz.github.io/nnqrg) [Nayuki's QR Code generator library](https://www.nayuki.io/page/qr-code-generator-library). instead of rolling my own.
