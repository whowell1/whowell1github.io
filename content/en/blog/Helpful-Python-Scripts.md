---
author: "Wren Howell"
title: Quick Python Scripts for Security Professionals
date: 08/12/2025 
description: "Helpful Python Scripts"
tags: ["Python, Useful Scripts "]
thumbnail: https://images.ctfassets.net/em6l9zw4tzag/oVfiswjNH7DuCb7qGEBPK/b391db3a1d0d3290b96ce7f6aacb32b0/python.png
---

During a recent triage, I had to brush up on my Python skills to try to automate some tasks that I had to do. Here are a few helpful Python scripts could be helpful for security professionals. This page will continue to be updated as I often times use the same scripts to manipulate data in similiar ways.

This first script reads a file with IPs and gets the unique IPs and stores them into a set and prints them out. In the example below, the strip method is invoked twice, the first to remove spaces, and the second time to remove the []. 




{{< css.inline >}}

<style>
.emojify {
	font-family: Apple Color Emoji, Segoe UI Emoji, NotoColorEmoji, Segoe UI Symbol, Android Emoji, EmojiSymbols;
	font-size: 2rem;
	vertical-align: middle;
}
@media screen and (max-width:650px) {
  .nowrap {
    display: block;
    margin: 25px 0;
  }
}
{{ $image := $resource.Fit "600x400" }}
</style>

{{< /css.inline >}}
