---
author: "Wren Howell"
title: "Learning from Setbacks"
date: 2024-02-26
description: "Battling Back from Setbacks in Cyber"
tags: ["Learning, developing, setbacks"]
thumbnail: https://breakintoenglish.com/wp-content/uploads/2019/03/Common-mistakes-in-English-to-avoid.png
---
   
**Perfection Is a Myth—Especially in Security**

As security practitioners, we are often called upon when things are broken or when people make mistakes. Whether that be people liking on malicious links or downloading malware, we are responsible for correcting the error. We are often the fixer, the person or people that an organization trusts with power. 

Over time, this responsibility can lead us to having a god complex. It’s not uncommon in high-stakes professions. I’ve seen it in cybersecurity, in traders, and in medicine. Because of this, there is an unrealistic expectation of us to be perfect in every situation and to perform perfectly at all times. 

This mindset creates an unrealistic expectation that we must always be perfect.

To anyone reading this:  

**Perfection is a myth.**  
Whether you're a doctor, a lawyer, or a cybersecurity professional, you will make mistakes. Mistakes are inevitable in any job, but especially in security.

In our world, especially in Digital Forensics and Incident Response (DFIR), we often see more false positives than true positives. New teams can get overwhelmed with alert fatigue that can lead to  critical alerts being missed. Mistakes happen—and most times, they uncover systematic weaknesses that need to be addressed.

**Some Mistakes I’ve Made**

**Missing Persistence**  

During one case, an infected machine used DLL injection to maintain persistence. I removed the malicious DLL, but missed another file that was executing from a non-standard folder. That file was being repeatedly launched by a scheduled cron job. I’d only solved part of the problem.

**Blanking on Scripting**  

In a job interview, I was asked to write a simple script. But anxiety and stress took over. I froze. Something I’d done a many times  before suddenly became impossible. The frustration spiraled and never recovered to be able to solve the problem.

 **Blocking Bitdefender**  

At one point, I saw an email flagged by Proofpoint that referenced Bitdefender. Without fully understanding the context, I blocked all Bitdefender URLs. This flooded the queue and added more work to the team.

Every time, I make a mistake, the same feeling of disappointment, self-doubt, and frustration occur.

I replay each scenario  in my head and ask myself, why did I do that, what was I thinking? 

I used to lose sleep over it—okay, I still lose sleep—but I’m getting better.

What has helped me overcome these setbacks when I have them is having  great teammates and coaches. They have taught me not to dwell in the mistake, and cognitively reframe it as a learning opportunity. 

**Everyone Has Off Days—even the Best**
 
A example would be Paul George. Paul George is one of the best players in his generation. He has multiple All-Star appearances and is a  franchise leader. But during the 2020 NBA playoffs in the COVID bubble, he had one of the worst games of his career. In Game 7 against the Denver Nuggets, he missed shot after shot that led to his team, the Clippers losing. 

After the game, I am sure he replayed every shot he missed in his head. I am sure he felt many of the same emotions that all of us feel after perceived failure: disappointment, sadness, frustration.  

As disappointed and frustrated that he was,  Paul George did not let that one game define him. The next season, he came back better and he had one of the best seasons in his career. 

The lesson here is that greatness is not absence of failure, because often times, the more ambitious the goal, the more likely we are to hit road block on the way. The ultimate measure of success is not the number of roadblocks, but the ability to to recover and try again. 

Learning from the Aforementioned Setbacks

**Persistence Blind Spot**  

I now make it a point to examine not just what’s malicious, but _where_ it’s executing from. Suspicious execution paths—non-standard directories, temporary folders, AppData—are now a routine part of my investigative checklist.

**Scripting Paralysis**

I am working on a page that is helpful for security professionals to use when doing a typical IR jobs. 

**Blocking Domains**

To avoid blocking common domains, I wrote a Python script that cross-references a domain against the Tranco top 10,000 list. If the domain is in this list the script raises a warning to help prevent business disruption. 

**Final Thoughts**

In a field where we are expected to contain threats and mitigate risk, it easy to believe that failure is unacceptable. However, cybersecurity professionals is a complex field with many moving parts that makes failure inevitable. 

The goal of a cybersecurity, and society as a whole, should not be to eliminate mistakes entirely, but to have systems, teams, and mindsets that are resilient in the face of failure. 

You are not their worst mistake, it is how you bounce back and learn from it. 

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
