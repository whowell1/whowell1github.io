---
author: "Wren Howell"
title: "Detecting Read Teaming By Threat Actors"
date: 2025-07-10
description: "Using Canary Tokens to Combat Read Teaming"
tags: ["honeypot, tripwire, honeytoken"]
thumbnail: https://www.yalepest.com/wp-content/uploads/2021/12/Hand-reaching-for-a-piece-of-cheese-in-a-mousetrap.jpg
---

With Scattered Spider in the news again for breaching insurance firms, they have proven once again that having an EDR system on endpoints is not enough. Once an attacker is able to get in through social engineering, threat actors like to look for sensitive information in an organization, like SharePoint, Confluence, code repos, chats, and JIRA. Of course, as security professionals, we preach about access control and the concept of least privilege. However, no matter how good clean-up attempts are, there will always be sensitive information stored somewhere because someone will inevitably a password in a place, where they are not supposed to. So instead of aiming for perfection, we can use the fact that sensitive information will be stored somewhere accessible to the public to catch potential threat actors by using canary tokens. The use of canary tokens can help catch threat actors performing some reconnaissance activity. 

**What is a canary?**

Think of a canary as a simple tripwire that is used when an attacker or an unauthorized user tries to access sensitive material. Canaries can come in many forms, like fake users, credentials, or passwords, but the key thing about canaries is that it has to look real and appealing to attackers. 

There are many different kinds of canaries that can be deployed, and there are many companies that have good products. Thinkst Canary is a great company that has canaries that are easy to deploy and are relatively inexpensive. 

Even though without having an official vendors, you can build canaries through fake credentials in SharePoint, Confluence, and include fake credentials in git repos as well. 

**Example using a canary in SharePoint and alerting in Sentinel**

Go to SharePoint, look for places that would look like places that people could store a username and password, and create a realistic-looking username and password. Alternatively, make a new folder where only the security team would know that it would be a decoy.  There should be more than one canary, but not too many to trigger false positives. Once these canaries are made, here is some KQL query to help with detection. 

OfficeActivity
| where Operation in "FileAccessed"
| where TimeGenerated > ago (100min)
| where ObjectId has "name_of_document"
| project TimeGenerated, UserId, Operation, ObjectId, SourceFileName, OfficeWorkload, Site_url, SourceFileName

There will have to be some normalizing of behavior based on the organization, but this is a good start. 

Once this detection triggers, look to see if the particular user's behavior was consistent with recon activity and gather context about the user. 

Some questions to consider when triaging this alert 

- Who is the user and what is their role?
- What other files did the user look for in SharePoint in a certain time period?
- Did they actively try to log into accounts?

**Final Thoughts**

Canary tokens are a great way to detect threat actors like Scattered Spider, insider threats, and Red Teams that use internal documentation to breach organizations and move laterally in the environment. By laying smarter traps, canaries tokens gives defenders a chance to catch the attackers before they make a significant impact. 



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
