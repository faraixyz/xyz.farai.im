---
title: Ever Seen an Excel File with 17,179,869,184 Cells?
description: Well I have and it was over 300 megabytes
publishdate: 2024-10-22T05:48:01+02:00
tech: [excel]
tags: [wtf]
draft: false
---

I ended up with a 318MB Excel file at work. It's a big problem but I don't have to use it much so I didn't care. I had to use it recently and I noticed Microsoft Excel provided suggestions to improve the file's performance. Clicking sheet by sheet I didn't see anything wrong until I came across this:

![Workbook Performance widget saying it checks for excess formatting, unneeded metadata and unused styles which cause slow workbooks. Also, optimizing the workbook won't affect data. Also mentions that 124,098,812 cells have been used where 123,939,622 of them can be optimized](/images/massive-excel.png)

No, it's not a bug—there were indeed over 100 million cells with styles which were weighing down the Excel file. Turns out the creator was trying to future proof cell borders and didn't realize that he selected every cell up to `XFD1048444` which reaches the column maximum (16,384) and is short of the row maximum (1,048,576) by about 940,000 cells. That's over 17 billion cells! While ~17 billion is the maximum, you can have as many sheets as your computer's memory allows. Then again, Excel mentions **used** cells rather than **styled** cells so I'm not sure what value was put in.

Fixing this reduced the file size by over 99% down to 1.2MB. Elon should hire me to solve [their compression algorithm](https://content.neuralink.com/compression-challenge/README.html).

*Also see: [How big PDFs can actually be](https://alexwlchan.net/2024/big-pdf/ '{"data-rel":"see-also"}') (spoiler alert: much larger than Germany)*
