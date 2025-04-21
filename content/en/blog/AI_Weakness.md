---
author: "Wren Howell"
title: "Addressing LLM Limitations "
date: 2025-04-12
description: "Weakness in LLMs"
tags: ["Prompt Injection, Hallucinations"]
thumbnail: https://eu-images.contentstack.com/v3/assets/blt6d90778a997de1cd/blt621ce6e29b55c494/670d41be3dbe55de0cb9db4b/LLM(1800)_Krot_Studio_Alamy.jpg?width=1280&auto=webp&quality=95&format=jpg&disable=upscale
---

The AI hype has finally gotten to me too.

I’ve been hesitant to write about AI because everything moves so fast—any post risks being outdated the moment it goes live. But lately, my LinkedIn feed has been flooded with mentions of MCP (Model Context Protocol). Engineers are testing it in real time, while the hype crowd celebrates it as the next big thing. Google also just announced its own AI protocol, A2A, which engineers will start experimenting with—and sales teams will no doubt amplify.

Despite the advancements in large language models (LLMs), two core issues remain unresolved: prompt injection and hallucinations.

**Prompt Injection**

A prompt injection attack occurs when an attacker manipulates the input to an LLM to make it produce unintended or harmful outputs. This can be done directly—by embedding malicious instructions in user input or indirectly, via third-party applications feeding compromised content into the model. This is a tough problem to fix because LLMs are inherently designed to trust their input. As LLMs become more integrated with tools and applications, the opportunities for prompt injection  increases significantly.

This is an inherent flaw that will be hard to fix because LLM are designed to trust the input of the LLM. As LLMs get more access to applications, the opportunities for prompt injection increase.

**Update [https://simonwillison.net/2025/Apr/11/camel/] April 13th via blog by Sam Wilson** 

Sam Wilson proposed a way to combat prompt injection. The big idea here is that there are two LLMs a privileged LLM and a Quarantined LLM. The role of the privilege LLM is only to see trusted content (in his example, it's user input) that can do real actions, that do not see untrusted data. The role of the quarantined LLM is to see untrusted data (in his example its email address and documents), but it is sandboxed and calls only extract information. The second part is that there is a control flow to show what the LLM is doing allowing the user to validate what the LLMs are doing to control execution flow in a Python-like language.

By having a two-layer system, this attempts to prevent dangerous data leaving, it adds some guardrails and transparency of the LLM's actions before anything harmful is done.

However, what this solution does not address is user fatigue. If a user has to validate every step that an LLM is trying to do, users could get tired of checking and blindingly press "yes" to everything. 

**LLM Hallucinations**

Hallucinations occur when an LLM generates incorrect or entirely fabricated information. This happens because LLMs don’t "know" facts—they’re just really good at predicting the next word based on patterns in their training data. Think of it as an ultra-powerful autocomplete, trained not on search terms, but on language itself.

The core problem? LLMs don’t know what data is good or bad. To them, it’s all just data. If misinformation was part of the training set—or structured similarly to credible content—it can just as easily be output as fact.


With new protocols emerging and AI tooling growing more complex by the day, it’s worth pausing to reflect on the tradeoffs. These systems are powerful, but they’re not bulletproof. And as defenders, we must stay just as creative and vigilant as the adversaries who are thinking up new ways to exploit them.

Let’s keep the promise—and limitations—of AI in focus without just focusing on the hype.



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
