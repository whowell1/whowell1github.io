---
author: "Wren Howell"
title: "Addressing LLM Limitations "
date: 2025-04-12
description: "Weakness in LLMs"
tags: ["Prompt Injection, Hallucinations"]
thumbnail: https://eu-images.contentstack.com/v3/assets/blt6d90778a997de1cd/blt621ce6e29b55c494/670d41be3dbe55de0cb9db4b/LLM(1800)_Krot_Studio_Alamy.jpg?width=1280&auto=webp&quality=95&format=jpg&disable=upscale
---

The AI hype has finally gotten to me too. I was hesitant to write about AI because things change so quickly that any post I have will likely be outdated soon after it is published. All I see on my LinkedIn timeline is MCP (Model Context Protocol). The engineers are testing this out in real-time and the AI hype people are praising it believing it will revolutionize everything. Google also announced its new AI protocol, A2A, that engineers will be experimenting with and salespeople will no doubt hype up. However, despite the advancements in LLM, there are two things that LLM has failed to address, which are prompt injections and hallucinations.

**Prompt Injection**

A prompt injection attack when an attacker manipulates the input to the LLM to trick it into producing unintended outputs. An attacker can directly manipulate the prompt by hiding malicious prompts or an attacker can indirectly hide malicious prompts via third-party applications.

This is an inherent flaw that will be hard to fix because LLM are designed to trust the input of the LLM. As LLMs get more access to applications, the opportunities for prompt injection increase.

**Update April 13th via blog by Sam Wilson**

Sam Wilson proposed a way to combat prompt injection. The big idea here is that there are two LLMs a privileged LLM and a quarantined LLM. The role of the privilege LLM is only to see trusted content (in his example, it's user input) that can do real actions, that do not see untrusted data. The role of the quarantined LLM is to see untrusted data (in his example its email address and documents), but it is sandboxed and calls only extract information. The second part is that there is a control flow to show what the LLM is doing allowing the user to validate what the LLMs are doing to control execution flow in a Python-like language.

By having a two-layer system, this system attempts to prevent dangerous data leaving the tool and it adds some guardrails to the execution of the prompt.

However, what this solution does not address is user fatigue. If a user has to validate every step that an LLM is trying to do, users could get tired of checking and blindingly press "yes" to everything.

**LLM Hallucinations**

LLM hallucinations are when LLMS generates wrong information. This is because LLMs are designed to predict the next word or next portion of a word based on patterns. LLMs predict the next word by analyzing the previous words and calculating the most statistically likely word to come next based on training data. It is basically an advanced recommendation system trained on words instead of Google searches. The primary weakness is the data that these LLMs are trained on. There is no way to validate between good and bad data because to an LLM it's all just data.

With AI tools exploding and new protocols being developed, it is important to stop and think about the tradeoffs we are making by using these tools. There will always be bad guys thinking about how to abuse these systems, so let us all stay vigilant on the promise and the limitations of our AI tools.


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
