---
author: "Wren Howell"
title: "Looking at Linux Persistence Mechanisms"
date: 2025-06-02
description: "Exploring Linux Persistence"
tags: ["Linux Persistence"]
thumbnail: https://miro.medium.com/v2/resize:fit:1400/0*Qqqd7UsfFDPL7WXh.jpeg
---

Recently, I had a to write a playbook on common persistent mechanisms. Even though there are lot of resources for this, I did not feel like recreating common persistence mechanisms playbooks on Linux again. This is not a comprehensive list of all the places that persistence can occur on Linux, but it is a start and order will be from most common locations to lesser known places. This page is going to be a work in progress as I add more persistence locations in the future. 

**What is persistence?**

Persistence is "the characteristic of a state that outlives the process that created it."
Breaking down the language in a more straightforward way, persistence is the ability of software, configurations, or data to remain even after the system is restarted or shut down. Persistence is essential for computers to run smoothly, but threat actors use persistence to maintain unauthorized access to a machine.

**What are some common Linux Persistence locations?**

There are also many places where persistence can occur in Linux as well. Some of the persistence mechanisms are similar to Windows, like cron jobs, but some are different. 

Some common Linux Persistence locations are listed below:

- Scheduled tasks through cron jobs 
- SSH
- Modifying start up scripts 
- Creation of accounts

**What is Cron job and where is it located?**

- Cron jobs are like scheduled tasks in Windows. They are used to schedule tasks to run at specific times or intervals and come on most Linux systems. Cron jobs can executed from both a system level and a user level so this is very common way that threat actors try to achieve persistence. The file locations of the crob jobs are located below.  

For user wide cron jobs:

  - /etc/crontab
  - /etc/cron.d/
  - /etc/cron.daily/
  - /etc/cron.hourly/
  - /etc/cron.monthly/
  - /etc/cron.weekly/

For system defined cron jobs:

 - /var/spool/cron/
- /var/spool/cron/crontabs/


**What is SSH and why is it used for persistence?**

SSH is a network protocol that is used for computers to connect with each other. SSH is one of the main ways that Linux computers network. One of the critical parts of the SSH is the authorized_keys file. This is a file that list of public keys that are allowed to log in to a given user account. Looking at this file is key to seeing if there is a unauthorized user trying to get access to account. 

The authorized keys in located in two directories 

- In the user directory:

```bash
~/.ssh/id_rsa
~/.ssh/id_rsa.pub
~/.ssh/authorized_keys
/root/.ssh/id_rsa
/root/.ssh/id_rsa.pub
/root/.ssh/authorized_keys
``` 

- In the system wide configs is at 

```bash
/etc/ssh/
``` 

To show when the authorized keys were added 

```bash
stat ~/.ssh/authorized_keys
```


**What are start up scripts and where are they located?**

Start up scripts are like autorun scripts in Windows and these programs run automatically when the system boot or when a user logs in. There are many scripts in Linux that are considered start up scripts. 

User Level

- ~/.profile
- ~/.bash_profile
- ~/.bash_login
- ~/.bash_logout
- ~/.bashrc



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
