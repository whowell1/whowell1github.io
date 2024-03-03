---
author: "Wren Howell"
title: "Exploring the HKCR Registry Key"
date: 2023-01-04
description: "HKCR Registry Key"
tags: ["HKCR Registry Key, Windows Registry Keys, Windows Internals"]
thumbnail: https://www.lifewire.com/thmb/vSIOZud80_RztuYM25I1lAdfto8=/750x0/filters:no_upscale():max_bytes(150000):strip_icc():format(webp)/hkey-classes-root-registry-8b4daed03243417daf82e54efc181834.png
---

 When I was visiting friends during Christmas break, a friend's relative was watching basketball on a streaming site. With his permission, I asked to see his laptop to check if any strange downloads were attempted, but nothing caught my eye initially. But I saw some peculiar extensions in the recycle bin. Since I knew that he only used the computer for surfing the internet and editing documents, I decided to do some proactive hardening for him. 

The Windows Registry is like a library that stores essential information about a computer's configuration settings, preferences, and settings. The library is broken up into different sections called Hives, each with a key and subkeys (where something is stored) and associated value (what is stored) within them.

A particular key, HKEY_CLASSES_ROOT\ in the Windows Registry, contains information related to file extensions. The purpose of this key is to manage the behavior and file associations in Windows. Every time a user tries to open a file on their computer, the operating system checks this key to see how to open it. For example, when a user tries to open a .txt file, Windows looks up how this application can be run (by default, it is via Notepad) and then determines how to edit and execute the file.

Since this behevior is all pre-programmed, as a user (or a system administrator), we can control how particular extensions will be executed when they are opened. This is important because threat actors use certain file extension types to get a user to execute a malicious program on a machine. One of the common file extensions that threat actors abuse is .hta extension. HTA stands for  Hypertext Markup Language Application that has an executable file that contains hypertext code and could also contain VBScript or JScript code.  Since threat actors commonly abuse.hta  file extensions,  changing it to open in a .txt file instead will buy the user some time to think and ask questions, e.g., Do I really want to execute this file? Changing these  defaults could prevent the user from executing the extension automatically. This is like having a friend, parent, or relative asking, 'Are you really sure you want to do this right now?' Just like when sometimes we need someone to avoid making regrettable mistakes, sometimes we need to change the defaults to help us avoid decisions that we could regret later. 


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
