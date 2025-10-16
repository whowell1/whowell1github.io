---
author: "Wren Howell"
title: "Evading EDR Through Device Codes" 
date: 2025-09-30
description: "Evading EDR through identity"
tags: ["Evading EDR, identity"]
thumbnail: https://media.licdn.com/dms/image/v2/C5612AQEDmE7dEsxqZQ/article-cover_image-shrink_720_1280/article-cover_image-shrink_720_1280/0/1541702431785?e=1763596800&v=beta&t=JUdJe7rv49SiBEwcmzgnPW1yp6b-AYrkYxvb8ST0BLQ
---

Cybersecurity is a game of cat and mouse between the threat actors and the cybersecurity professionals. Ten years ago, most companies did not have endpoint security systems so threat actors were able to install malware on systems. When EDR started to get installed on enterprise endpoints to be able to identify malware, threat actors moved to using living off the land techniques to move stealthily in environments. After Covid-19, as more companies moved to the cloud, threat actors were able to see that it was easier to log in than to break in. This shift gave rise to the phrase that defines today’s threat landscape:

**Identity is the new perimeter**

In this post, we’ll explore how threat actors can use the Device Code authentication flow in Azure to gain initial access.

**What is Device Code Authentication?**

Device code flow lets you sign into devices that lack local input devices, like shared devices or digital signage. This was designed when for signing in on devices that lack an input method, like a keyboard, by using a temporary code and a separate device with a browser to complete the process. 

**How Threat Actors Exploit Device Code Authentication in Azure**

1) Send a post request to https://login.microsoftonline.com/common/oauth2/devicecode?api-version=1.0 with a client_id and resource_id. 
2) Send a user the phishing email with legit Microsoft URL and device code on it
3) Retrieve the access token and refresh token from the compromised user. 

This is a little different from traditional phishing attacks because there is not a suspicious url or domain to block, the whole attack flow uses Microsoft hosted infrastructure that makes it more difficult to spot.

**What are Access Token and Refresh Tokens in Azure?**

Access token
-  They are short-lived credentials issued by Microsoft Entra ID that allow a client (an application) to authenticate and access specific resources or APIs (Microsoft Graph, Azure Resource Manager, or a custom API you’ve protected with Entra ID).  
- Access tokens are issued in the form of a JWT (JSON Web Token) and typically expire after about an hour.

Refresh Tokens 
-  They are long-lived credentials issued by Microsoft Entra ID that allows a client application to get a new access token without asking the user to sign in again.

**Detection Ideas: Spotting Device Logins**

Endpoint Forensics in the browser 
-  Look at browser history and see the links to https://microsoft.com/devicelogin. Combine this artifact with additional artifacts using Sign-in logs. 

Sign-in logs
- Look for where the authentication method is Device Login
- Look for newly registered devices or devices that are non-managed in Intune that have been registered.
- Look for anomalous IP addresses that are not associated with the user.


**Mitigating Device Flow Authentication** 
- The most effective defense is implementing Conditional Access policies that restrict sign-ins to approved and compliant devices only. Having additional policies like disabling device code authentication for applications that not require it, using MFA for all logins, monitoring unusual device registration can also help mitigate this threat. 


Resources 

- https://www.volexity.com/blog/2025/04/22/phishing-for-codes-russian-threat-actors-target-microsoft-365-oauth-workflows
- https://aadinternals.com/post/phishing
- https://dirkjanm.io/phishing-for-microsoft-entra-primary-refresh-tokens
- Xintra 


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
