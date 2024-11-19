---
title: Initial Impressions of My New Laptop After Using It For A Month
tags: [pc]
publishdate: 2021-06-14T18:08:35+02:00
lastmod: 2024-10-20T18:52:00+02:00
description: My sister brought me a new laptop to replace my 5 year old one. Here's what I think of it so far.
draft: false
---

For the past 5 years, I've been using my [**HP Pavillion 15t**](https://web.archive.org/web/20170909005551/https://agckb.wordpress.com/2015/12/31/setting-up-my-new-laptop/) which has no battery and lots of dents. Despite the battery it worked fine though it would be nice to get a new laptop. That wish came true when my sister came home for a holiday and she bought me a new laptop, an **HP Pavillion x360 14**. I've been using it for a month now and these are my thoughts and how they stack up against the 15t.

## Very First Impression and Set Up

As I got the laptop the first thing I noticed was just how thin it was. Along with being thin, it had a decent selection of ports with 2 USB Type A 3.1 Gen 1 ports, an SD card slot, HDMI 2.0 and a USB Type 3 Gen 2 port. It would be nice if the USB C port was Thunderbolt, but I don't have any Thunderbolt devices so it isn't an issue for now.

It also came with a power brick with a Type G (UK) and Type C/E/F (EU) plug. Since I already have a Type B plug (US), I'm well prepared for global travel (once that's possible).

Starting it up for the first time, I was greeted with a lot of crapware. I thought factory resetting it would delete it but it didn't so I had to manually install it which was harder than I thought since it didn't recognize the laptop's storage media. If you plan on doing that, make sure you download the laptop's storage drivers or the installation won't find a partition. 

## Display, Pen and Webcam

Having gotten the installation out of the way I could focus on the 14" IPS screen. Not sure it's the glossy finish but I like how the screen looks. Shame it isn't very bright which makes it terrible in the sun. It's also a touchscreen which is more useful than I expected. There's a pen, though I don't use it much. Compared to my Apple Pencil, it's got some noticable input lag (if I do the squiggle test), though it's still usable.

I can't say much about the webcam since I don't use it but the only good thing I can say about it is that it exists. Nothing good about 720p.

## Keyboard and Trackpad

Typing on the keyboard feels great but it doesn't have a backlight which I took for granted. One problem I had was that I couldn't enter special characters with alt codes since I didn't have a numpad. ~~I fixed it thanks to [Stack Exchange and AutoHotKey](https://superuser.com/a/448304). I should use [AutoHotKey](https://www.autohotkey.com/) more.~~<span id="more"></span>++**Update 20 October 2024** I now use [QuickAccent from PowerToys](https://learn.microsoft.com/en-us/windows/powertoys/quick-accent) instead++.

While the keyboard is nice, the trackpad isn't. It would be fine if I could use my own mouse, but the lag was terrible. Thankfully I kept the unifying receiver so I'm connecting the mouse which leaves me with one less USB port.

## Performance

The x360 comes with an 11th Gen Intel i5 processor which is a huge step up from the 6th Gen Skylake i5 in the 15t. Honestly I don't feel much of a difference when I'm doing my usual computing. SSDs do a lot to make a laptop snappy. To push the laptop, I did the most CPU intense thing I know—video transcoding.

I download YouTube videos instead of watching them online. I need to transcode them to make them fit on my 64GB iPad. As a test, I got 20 hours of videos ecoded in various formats and transcoded them into mp4s with HEVC video and opus audio at a `veryfast` preset. The 15t did it in **6 hours 57 minutes** where the x360 did it in **3 hours 57 minutes**! That's 42% faster.

This is great but I'm a bit disappointed that it couldn't do better even though it totally could. Looking at the CPU utilization graphs, the 15t run at max CPU forever whereas the x360 sticks around 80–85%. 

![Two CPU Graphs with the i5-6200U at 100% utilization and 2.69GHz and the i5-1135G7 at 85% utilization and 2.76GHz](/images/6v11-cpu.png)

The x360 is still faster, but I can't help but think how much better it would be if I could get that extra 15%. It's been a problem with Intel for the past few years and the competition from AMDs Ryzen and more recently Apple's M1 are shaking things up, being more performant at less power. Regardless, I'm happy with the x360s performance. I also tried to encode some 4K video at it ran at 1fps which is dredful but that's ten time faster than the 15t.

I looked into possible ways to improve performance and I came across **undervolting** and **reapplying thermal compound**. [Unvervolting isn't possible due to security issues](https://www.notebookcheck.net/Intel-and-OEMs-have-killed-undervolting-and-there-is-little-that-you-can-do-about-it.477330.0.html) and I can't afford let alone get thermal compound nor am I willing to open up my laptop to apply it.

## Battery

My perception of the battery isn't very good since I came from having no battery so all I can say is that I'm glad it exists. One thing that I wish I could do is to cap the charge level at 50% so I can safely use it plugged in while prolonging the battery's life. Alas, that can only be done on HPs business laptops. 

## Issues

There are some QC issues as I'm using the laptop. As I said connecting things through bluetooth is buggy. Also the laptop gets hiccups once in a while, briefly freezing and grating before carrying on. I remember the 15t having that issue so I'm sure it'll go away with time.

## Conclusion (for Now)

It's about time I replaced my 15t and the x360 is good enough. While I wish I knew I was going to get a laptop so I choose the one I wanted, I'm happy that I don't have to worry about nudging the batter. I'm satisfied with the performance, enjoy the touchscreen and typing experience though it really needs a backlit keyboard, a brighter screen, Thunderbolt (though I don't need it) and stricter quality control.

I might write about this laptop some more in the future but for now, you can read these posts on me setting up the older 15t.

* [Setting Up My New Laptop](https://web.archive.org/web/20170909005551/https://agckb.wordpress.com/2015/12/31/setting-up-my-new-laptop/)
* [Setting Up My New Laptop – Part 2](https://web.archive.org/web/20170909005804/https://agckb.wordpress.com/2016/01/08/setting-up-my-laptop-part-2/)
