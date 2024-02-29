---
author: "Wren Howell"
title: "Mac Persistence Mechanisms"
date: 2024-01-25
description: "Mac Persistence"
tags: ["Mac Persistence, Launch Daemon, Launch Agent"]
thumbnail: https://1000logos.net/wp-content/uploads/2016/10/apple-emblem.jpg
---

Recently I had a friend that was concerned about some strange behavior that was occuring on his Macbook, so I decided to look at common persistence mechanisms on a Mac host. I remember when I first got my Macbook, one of the selling points was that "Macs do not get any virus." Sadly this is no longer true, and the types of malware that affect Macs are growing. Here is a background on Mac persistence mechanisms from The Art of Mac Malware by Patrick Wardle. This is only going to be basics as it will only cover persistence mechanisms in launch daemon and launch agents.


**What is persistence?**

Persistence is defined as ‘the characteristic of a state that outlives the process that created it.
Breaking down the language in a simpler way, persistence is the ability of software, configurations, or data to remain even after the system is restarted or shut down. Persistence is essential for computers to run smoothly but threat actors use persistence to  maintain unauthorized access to a machine.

**What are Launch Agents and Launch daemons?**

A launch daemon is like a housekeeper who works quietly in the background, taking care of essential tasks that keep the house running smoothly, even when nobody is home. Just like a housekeeper that manages critical things in a house, a  launch daemon manages important system processes, like handling network connections ensuring they're always available to keep the computer running smoothly. On the other hand a launch agent is more like a personal assistant that reminds you about the doctor appointments and events. Similar to the personal assistant, a launch agent only handles tasks that are relevant only to that user. 

A good comparison of launch agent and launch daemons in Windows would be Windows Services or scheduled tasks. However instead of storing things in the registry hive, because it is a Mac launch agent and launch daemons store its data in a property list (plist) file. Plists are used to store configuration settings, preferences, and metadata for applications and system components in macOS. 

**Where are Launch Agents and Launch Daemons located?**

- ~/Library/LaunchAgents for user specific settings
- /Library/LaunchDaemon for System-wide setting

**Potential Solution?**

When looking at the metadata of the plist, there are some keys that may offer a clue into a program having persistence. Those keys are

- RunAtLoad:if this is set to true, it will run automatically when the machine turns on. Like a cron job
- KeepAlive: if this is set to true, the program will restart if it dies
- StartInterval: if this is present, it will specify a time interval (in seconds) for the program to be relaunched.

What I told my friend is to look at programs running from the directories in launch daemon and launch agent. Are there any programs that he does not recognize? Are there any programs running where any of the plist flags do not make sense?

To make analysis easier for him, I made a small [python](https://github.com/whowell1/Mac-Persistence-Simple/blob/main/mac_persistence_checker.py) program that displays the directories where launch daemon and launch agents are, and looks for the hash of the program. I told him to check the hashes of each file and if they do not show up in Virustotal, then he has something that needs to be investigated more. 


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
