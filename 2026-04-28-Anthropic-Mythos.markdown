---
layout: post
title:  "Lessons from the Mythos Crisis Cell: Risk, Ownership, and Overreaction in AI Security"
date:   2026-04-28 13:25:40 -0400
categories: AI
---

*A personal account from inside the response.*

## What Is Mythos?

Mythos is an AI system developed by Anthropic with offensive cybersecurity capabilities. Concretely, it can assist with tasks that fall squarely in the domain of offensive security: identifying vulnerabilities, reasoning about attack surfaces, and executing actions that a skilled attacker might perform. It is not a chatbot with a security plugin. It is a system purpose-built to operate in that space.

Access to Mythos is, by design, restricted. This is not a consumer product. Only a handful of organizations have or would have access to it, under controlled conditions. That context matters enormously when evaluating the risks, though it was largely absent from the loudest conversations.

## What the Community Said

When word spread about Mythos's capabilities, the reaction was swift and, in many corners, severe. The concerns raised fell into a few recurring categories.

The first was that the model was simply too dangerous to exist in deployable form. The argument: an AI system capable of offensive security tasks represents a qualitative leap in what attackers can do, and no governance framework is mature enough to contain that risk. Publishing it, or even deploying it in restricted form, would set a precedent that others would follow with fewer safeguards.

The second concern was about access concentration. The fact that only select companies would have access was framed not as a safeguard, but as a fairness and power problem. Who decides which organizations are trusted enough? What happens when those organizations are themselves compromised or act in bad faith?

The third, and most technically grounded concern, was about capability uplift: that Mythos would lower the barrier to entry for sophisticated attacks, enabling actors who previously lacked the expertise to execute complex intrusions.

These are not unreasonable concerns to raise. They deserve to be taken seriously, evaluated against evidence, and answered with specificity. What happened instead was something different.

When Anthropic's Mythos project triggered an internal crisis response, I had a front-row seat. What followed was one of the most instructive, and at times frustrating, experiences i've had working at the intersection of AI and security. 

I've spent enough time in environments where the value of intelligence depends entirely on who holds it and what they can do with it to recognize when a threat is being inflated beyond what the signal actually supports. This post is my attempt to process it honestly, for the benefit of anyone building, deploying, or governing AI systems with cybersecurity capabilities.

## The Panic Was Real. The Threat Model Wasn't.

The first thing I noticed was how fast the alarm spread, and how little of it was grounded in a concrete threat model.

People were reacting to the *existence* of a capability, not to a realistic attack scenario. In security, this is a critical distinction. The relevant question is never "could this be misused in theory?" It's "under what conditions does misuse actually become feasible, and how likely are those conditions?"

For Mythos, the answer is fairly clear: **the system poses meaningful risk only if an adversary has access to the source code.** Without that, the attack surface is dramatically reduced. Most threat actors, even sophisticated ones, are operating against black-box systems. They don't have the internals. The panic, in large part, was disconnected from this reality.

This doesn't mean the risk is zero. It means the risk was being evaluated without the rigor that security decisions require.

## The Ownership Problem: Nobody Wanted to Decide

One of the most operationally damaging dynamics I witnessed was the absence of a clear decision owner.

When everyone is responsible, no one is. Every stakeholder had opinions. Legal was cautious. Engineering was defensive. Leadership wanted consensus. The result was a decision-making process that moved at the speed of the most risk-averse voice in the room, which in a crisis is rarely the most informed one.

In incident response and crisis management, **designated authority matters more than broad agreement**. You need someone who can say "here is our decision, here is why, and here is who is accountable." Without that, you get endless rounds of escalation, hedging, and delayed action, all while the actual risk window either closes or compounds.

If your organization is deploying AI capabilities with security implications, assign ownership before the crisis, not during it.

## Risk Assessment Should Precede Deployment, Not Follow Escalation

This is the structural lesson I keep coming back to.

The crisis cell existed because a risk assessment hadn't been done with sufficient rigor before the capability shipped. When the alarm went off, people were trying to evaluate the risk in real time, under pressure, with incomplete information, and with organizational incentives that biased toward caution regardless of the actual threat.

A proper pre-deployment security review for a capability like Mythos should include:

- **Threat modeling with realistic attacker profiles.** Who actually has access? What do they already know? What would they need to exploit this?
- **Dependency on source code access.** If the capability requires internal knowledge to weaponize, that changes the risk calculus significantly.
- **Clear escalation criteria.** Define in advance what would constitute a genuine incident versus a theoretical concern.
- **A named owner.** One person or team accountable for the risk decision.

None of this is novel. It's standard practice in mature security organizations. The gap is in applying it consistently to AI systems, where the novelty of the technology tends to bypass existing governance processes.

## What I Actually Believe About Mythos

Let me be direct: I don't think Mythos is a reckless project. I think it got caught in a governance gap, the kind that opens up when a capability advances faster than the institutional processes designed to evaluate it.

The cybersecurity capabilities in question are only as dangerous as the access an adversary has to the underlying system. In most realistic deployment scenarios, that access doesn't exist. The risk, while real, is bounded, and bounded risks can be managed with targeted mitigations rather than broad freezes.

What concerns me more than the capability itself is the precedent set by a crisis response that wasn't anchored to a rigorous threat model. If we overreact to bounded, source-code-dependent risks, we build a culture where the loudest concern wins, not the most defensible one.

That's a problem for AI security in the long run.

## Slow Down Before You React

None of this is an argument for complacency. Mythos operates in genuinely uncharted territory. Offensive AI capabilities are new enough that the boundaries of what's possible, and what's exploitable, are not fully understood. That uncertainty is real, and it deserves respect.

But uncertainty is not the same as emergency. And novelty is not the same as unmanageable risk.

What the Mythos crisis cell revealed, more than anything, is that the security community still doesn't have a reliable reflex for sitting down, thinking clearly, and applying proportionate mitigations when a new AI capability surfaces. The reflex we have instead is to escalate, to freeze, and to let the loudest voices set the tempo. That reflex is understandable. It is also costly.

The work of AI security governance is not glamorous. It's threat modeling at 9am on a Tuesday. It's a document that nobody reads until something goes wrong. It's the uncomfortable conversation about what risk level is actually acceptable, made before deployment, not after. That work doesn't feel urgent until the moment it becomes the only thing that matters.

Mythos may be new. The playbook for handling it doesn't have to be invented from scratch every time an alarm goes off. Take the time to sit down. Think through the actual threat model. Apply mitigations that match the real risk. Then move forward.

Panic is not a security strategy.

*The views expressed here are my own and do not represent my employer official position. Details have been generalized to respect confidentiality.*