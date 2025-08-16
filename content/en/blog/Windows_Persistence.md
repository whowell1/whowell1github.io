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
- DLL Hijacking
- Services 
- WMI
- Powershell profiles


**What is AutoRun and where is it located?**

- Auto run are programs or applications that are designed to run automatically when operating system or the user logs in. AutoRuns are also referenced as  AutoStart Extension Points (ASEPs). There are over 50+ places where maliware can run, but many of these are located in the Registry. 

Just a quick reminder, a Windows Registry is a database where Windows stores all the configurations for users, applications, system, and hardware. 

Common Registry keys that have Windows malware establish persistence in a single user is: 

- NTUSER.DAT\Software\Microsoft\Windows\CurrentVersion\Run
- NTUSER.DAT\Software\Microsoft\Windows\CurrentVersion\RunOnce

Common Registry keys that have Windows malware establish persistence in all users are: 

- Software\Microsoft\Windows\CurrentVersion\Run
- Software\Microsoft\Windows\CurrentVersion\RunOnce
- Software\Microsoft\Windows\CurrentVersion\policies\Explorer\Run
  - This is a group policy based auto-run location 

Another common place where persistence occurs is in the Windows Start up folder. Any programs in this folder will execute when a user logs on. 

Location for the Start Folder is located below:

- %AppData%\Roaming\Microsoft\Windows\Start Menu\Programs\Startup 


**What are Scheduled Tasks?**

```bash
C:\Windows\System32\Tasks\
```
Scheduled Tasks or Task Scheduler is a built-in Windows utility that allows users to automate the execution of programs, scripts, and various tasks at specific intervals or specific events. 

Schtasks.exe is a Windows command-line application for managing scheduled tasks on local or remote computers, such as creating, removing, editing, executing, and terminating tasks. 

Threat actors install programs in scheduled tasks at certain intervals to execute at particular time to try to evade detection by blending in with other start up programs. 

A way to 

**What is DLL Hijacking?**

DLL Hijacking abuses legit features of the Windows OS. Some examples of DLL Hijacking are DLL Search Order Hijacking, Phantom DLL Hijacking, and DLL Side Loading. 

  - DLL Search Order is a technique where a attacker tricks a program into loading a malicious DLL instead of the legit one. When a program in Windows runs, it does not know the location of where the DLL (a piece of code is located). Because the program does not know where the DLL is, it follows a search order to find it. If an attacker is able to load a DLL in one of the searched folders (where the executable lives, or in the System32 directory), an attacker can load the malicious DLL. 

  - Phantom DLL Hijacking is a technique where attacker uses a DLL that no longer in the Windows operating systems or not neccessary. When a attacker is able to do this, this can lead to code execution. 

  - DLL Side Loading is an attack where the attacker loads a legit exe with a malicious dll in the same folder because the EXE does not specify a full path. DLL Side loading abuses a Windows feature where a a new DLL gets loaded onto the path of a executable. This new DLL has a no validity checks that allows the malicious DLL to run. A analogy to give for DLL Side Loading is getting catfished on a dating app. The person that you match with has great pictures and is attactive in a conventional way. However, when you meet up with the person you matched with looks nothing like the person in the picture. 


**What is Windows Services?**

Windows Services are programs that are intended to run in the background without user interaction. Services are required to run when the operating systems first start up as either executables or are DLLs. If the computer was a TV network like ESPN, the Windows Services would be the backroom staff that would make the broadcast go smoothly. 

Because there are so many types of Windows Services running, they are implented as DLL's or executables to save resources. When the operating system is running, it is normal to see several instances of svchost.exe, a generic Windows host process, running in the background. 

Another type of Windows service is the  Windows service control manager (services.exe) which is an interface to manage and manipulate services. The service control manager is accessible to users via GUI components as well as system utilities such as sc.exe and net. 

The Service Registry Keys are located at:

- HKLM/System/CurrentControlSet/Services  

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
