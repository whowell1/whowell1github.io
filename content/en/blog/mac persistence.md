---
author: "Wren Howell"
title: "Mac Persistence Mechanisms"
date: 2024-03-10
description: "Exploring Mac Persistence"
tags: ["Mac Persistence, Launch Daemon, Launch Agent"]
thumbnail: https://1000logos.net/wp-content/uploads/2016/10/apple-emblem.jpg
---

Recently, I had a friend concerned about some strange behavior on his Macbook, so I decided to look at common persistence mechanisms on a Mac host. When I first got my Macbook, one of the selling points was that "Macs do not get any virus." Sadly, this is no longer true, and the types of malware that affect Macs are growing. Here is a background on Mac persistence mechanisms from The Art of Mac Malware by Patrick Wardle. This post will only cover persistence mechanisms in launch daemon and launch agents.

**What is persistence?**

Persistence is "the characteristic of a state that outlives the process that created it."
Breaking down the language in a more straightforward way, persistence is the ability of software, configurations, or data to remain even after the system is restarted or shut down. Persistence is essential for computers to run smoothly, but threat actors use persistence to maintain unauthorized access to a machine.

**What are Launch Agents and Launch daemons?**

A launch daemon is like a housekeeper who works quietly in the background, taking care of essential tasks that keep the house running smoothly, even when nobody is home. Like a housekeeper who manages critical things in a house, a launch daemon manages important system processes, like handling network connections, ensuring they're always available to keep the computer running smoothly. On the other hand, a launch agent is more like a personal assistant that reminds you about doctor appointments and events. Like the personal assistant, a launch agent only handles tasks relevant to that user. Just like you only want trusted people to be your housekeeper and personal assistant, it is essential to have authorized launch agents and daemons to run on a Macbook.

A good comparison of launch agents and launch daemons in Windows would be Windows Services or scheduled tasks. However, launch agents launch daemons and store their data in a property list (plist) file instead of storing things in the registry hive. Plists are used to store configuration settings, preferences, and metadata for applications and system components in macOS.

**Where are Launch Agents and Launch Daemons and Where are They located?**

- ~/Library/LaunchAgents for user specific settings
- /Library/LaunchDaemon for system-wide settings

**Potential Solution?**

When looking at the metadata of the plist, there are some keys that may offer a clue into a program having persistence. Those keys are

- RunAtLoad: if this is set to true, it will run automatically when the machine turns on. This is like a cron job.
- KeepAlive: if this is set to true, the program will restart if it dies.
- StartInterval: if this is present, it will specify a time interval (in seconds) for the program to be relaunched.

I told my friend to look at programs running from the directories in the launch daemon and launch agent. Are there any programs that he does not recognize? Are any programs running where any plist flags do not make sense?

To make analysis more manageable for him, I made a small [python](https://github.com/whowell1/Mac-Persistence-Simple/blob/main/mac_persistence_checker.py) program that displays the directories where the launch daemon and launch agents are and look for the hash of the program. I told him to check the hashes of each file and if they do show up in Virustotal as malicious, he potentially has something that needs to be looked into further.




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
