---
author: "Wren Howell"
title: "Looking at Windows Persistence Mechanisms"
date: 2025-05-10
description: "Exploring Windows Persistence"
tags: ["Windows Persistence, Registry keys"]
thumbnail: https://www.bleepstatic.com/content/hl-images/2021/07/23/Windows-attack.jpg
---

Recently, I had a to write a playbook on common persistent mechanisms. Even though there are lot of resources for this, I did not feel like recreating common persistence mechanisms playbooks on Windows again. This is not a comprehensive list of all the places that persistence can occur on Windows, but it is a start and order will be from most common locations to lesser known places. This page is going to be a work in progress as I add more persistence locations in the future. 

**What is persistence?**

Persistence is "the characteristic of a state that outlives the process that created it."
Breaking down the language in a more straightforward way, persistence is the ability of software, configurations, or data to remain even after the system is restarted or shut down. Persistence is essential for computers to run smoothly, but threat actors use persistence to maintain unauthorized access to a machine.

**What are some common Windows Persistence locations?**

Some common Windows Persistence locations are listed below:

- Auto Run 
  - Includes places in the Windows Registry 
  - Includes Windows Startup folder
- Scheduled tasks
- Services 
- DLL Hijacking
- WMI
- Powershell profiles.


**What is AutoRun and where is it located?**

- Autostart are programs or applications that are designed to run automatically when operating system or the user logs in. AutoRuns are also referenced as  AutoStart Extension Points (ASEPs). There are over 50+ places where maliware can run, but many of these are located in the Registry. 

Just a quick reminder, a Windows Registry is a database where Windows stores all the configurations for users, applications, system, and hardware. 


Common Registry keys that have Windows malware establish persistence in a single user is: 

- NTUSER.DAT\Software\Microsoft\Windows\CurrentVersion\Run
- NTUSER.DAT\Software\Microsoft\Windows\CurrentVersion\RunOnce

Common Registry keys that have Windows malware establish persistence in a all users are: 

- Software\Microsoft\Windows\CurrentVersion\Run
- Software\Microsoft\Windows\CurrentVersion\RunOnce
- Software\Microsoft\Windows\CurrentVeersion\policies\Explorer\Run
 - This is a group policy based auto-run location 

Another common place where persistence occurs is in the Windows Start up folder. Any programs in this folder will execute when a user logs on. 

Location is

- %AppData%\Roaming\Microsoft\Windows\Start Menu\Programs\Startup 


**What are Scheduled Tasks and where is it located?**

```bash
C:\Windows\System32\Tasks\
```
Scheduled Tasks or Task Scheduler is a built-in Windows utility that allows users to automate the execution of programs, scripts, and various tasks at specific intervals or specific events. 

Schtasks.exe is a Windows command-line application for managing scheduled tasks on local or remote computers, such as creating, removing, editing, executing, and terminating tasks. 

Some of the reasons that actors install programs in scheduled tasks at certain intervals to execute at particular time, to try to evade detection by blending in with other starts. 



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
