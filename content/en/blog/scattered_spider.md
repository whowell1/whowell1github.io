---
author: "Wren Howell"
title: "Scattered Spider Hygiene"
date: 2025-05-02
description: "Scattered Spider"
tags: ["Social Engineering, Scattered Spider"]
thumbnail: https://www.crowdstrike.com/content/dam/crowdstrike/www/en-us/wp/2023/01/0123_01_SCATTERED-SPIDER_Blog_1060x698.jpg
---
In a previous post, we discussed how threat actors evade EDR (Endpoint Detection and Response) using Living Off the Land (LoL) techniques. In this post, I want to focus on threat actors who bypass EDR completely, called Scattered Spider. This group evades EDR completely by using social engineering tactics to cause harm to many organizations and has been behind the breaches of MGM, Twilio, and, more recently, Marks & Spencer in the UK. 

Some of their tactics are listed bullet points.

Impersonation and Phishing:

- Scattered Spider often starts their attack by calling legitimate staff members, and impersonating colleagues or IT personnel. They request password resets or one-time passcodes to gain access to critical systems. This method capitalizes on the human element and bypasses the need for brute-forcing credentials.

Bypassing Multi-Factor Authentication (MFA):

- Scattered Spider often uses technique called MFA fatigue to bypass multi-factor authentication. MFA fatigue when the the threat actor sends multiple prompts to the victim's phone to accept the login. By overwhelming employees with continuous MFA prompts, they can force a user into approving malicious login attempts. 

Remote Access Tools (RATs):

- Once inside the network, the group installs remote access tools like Anydesk, Fleetdeck.io, ScreenConnect, and Splashtop. These tools give them complete control over compromised systems, allowing them to exfiltrate data, move laterally, and maintain persistence within the network.

Looking for Passwords:

- In large organizations, sensitive information such as passwords and credentials is often stored in places like SharePoint or Git repositories. Once they gain initial access, Scattered Spider can locate these stored credentials and use them to move laterally within the network, escalating their privileges and accessing more critical systems.

Countering Scattered Spider’s Tactics

What can organizations do to better defend against these kinds of attacks? Here are some strategies:

Domain Impersonation Detection:

- Organizations should actively monitor for domain impersonation attempts (e.g., fake URLs that resemble legitimate ones). Threat actors often use lookalike domains (such as victim name-sso.com) to lure victims into revealing sensitive information.

FIDO2 MFA:

- To counter MFA fatigue, organizations should implement FIDO2-based MFA, which uses hardware keys or biometric authentication. This kind of MFA is resistant to phishing and MFA fatigue attacks, making it much harder for attackers to bypass.

Remote Monitoring and Management (RMM) Tools:

- Since remote access tools (RATs) are commonly used by threat actors to maintain control over compromised systems, it’s critical to monitor for suspicious use of Remote Monitoring and Management (RMM) software. This is particularly hard in global organizations where there are preferences for RMM that vary by region. A good first step would be to control who has the ability to download RMMs and choose RMMs that have some logging. Another tip for responders is to see how the user got the RMM on the endpoint, as that will give responders a clue if the RMM was downloaded for legit purposes or not. 

Phishing Simulation Training:

- Regularly conduct phishing simulations to test employee awareness and reinforce safe behaviors. Employees should be trained to recognize and report phishing attempts and suspicious interactions.

Look for Exposed Passwords:

- Do not make it easy for threat actors to look for passwords that are stored in Sharepoint/teams. A good tool that can help look for passwords in an enterprise setting is Cylera. 

**Conclusion**

Scattered Spider demonstrates the growing trend of threat actors who use social engineering to bypass EDR systems. Scattered Spider shows that security is not just a technical issue, but a multifaceted issue that needs support across departments.  


References

- https://www.sans.org/blog/defending-against-scattered-spider-and-the-com-with-cybercrime-intelligence/
- https://www.cisa.gov/sites/default/files/2023-08/CSRB_Lapsus%24_508c.pdf
- https://www.cisa.gov/sites/default/files/2023-11/aa23-320a_scattered_spider_0.pdf

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
