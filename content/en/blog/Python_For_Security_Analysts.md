---
author: "Wren Howell"
title: "Quick Python Scripts for Security Professionals"
date: 2025-08-10
description: "Helpful Python Scripts"
tags: ["Python, Useful Scripts"]
thumbnail: https://loudbench.com/wp-content/uploads/2023/02/Python-logo-1024x576.png
---

During a recent triage, I had to brush up on my Python skills to try to automate some tasks that I had to do. Here are a few helpful Python scripts could be helpful for security professionals. This page will continue to be updated as I often times use the same scripts to manipulate data in similiar ways.

This first script reads a file with IPs and gets the unique IPs and stores them into a set and prints them out. In the example below, the strip method is invoked twice, the first to remove spaces, and the second time to remove the []. This script can be modified to a users needs. In this case, the data was looked like: ["12.21.13.23"], with no other data. 

```python
cleaned_ips = set()

with open("ips.txt", "r") as f:
    for line in f:
        ip = line.strip().strip("[]")  
        cleaned_ips.add(ip)

# Print distinct IPs
for ip in cleaned_ips:
    print(ip)
``` 

There are many other variations of the code of this that can be useful as well. What if instead of priting all the unique ips in the data, you also want to count the number of IPs in the list? A len method can be invoked in the cleaned_ip set. 

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
</style>

{{< /css.inline >}}
