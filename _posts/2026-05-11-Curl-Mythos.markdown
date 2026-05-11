---
layout: post
title:  "When Hype Meets curl"
date:   2026-05-11 12:00:00 -0400
categories: AI
tags: AI
---

## What the Numbers Say

[Stenberg's post](https://daniel.haxx.se/blog/2026/05/11/mythos-finds-a-curl-vulnerability/) is worth reading in full, but the core is simple. Mythos analyzed 178,000 lines of C code. It surfaced five purported vulnerabilities. After review by the curl security team, four were dismissed as false positives or minor bugs. One was confirmed, rated low severity, and scheduled for disclosure with curl 8.21.0.

One. In a codebase with 188 published CVEs on record, continuous OSS-Fuzz coverage and multiple paid audits accumulated over years. Stenberg's conclusion is direct: the hype was primarily marketing.

I expected the results to be more modest than the framing. I didn't expect them to be this modest.

## The Hardest Possible Target

Part of what makes this result so telling is the choice of target. curl isn't a greenfield codebase or an enterprise application where security has been an afterthought. It's 178,000 lines of C written by 573 people over decades, maintained by someone who has spent years staring at its attack surface. If the case for Mythos being "dangerously good" at vulnerability discovery holds anywhere, it has to hold against something like this. The results say it doesn't.

Stenberg also noted that earlier AI tools, AISLE, Zeropath, OpenAI's Codex Security, produced hundreds of bugfixes against curl. Mythos produced one confirmed finding. That comparison appeared nowhere in the coverage that drove the original panic.

The hardest part of being in that crisis cell was arguing for proportionality when the room had already decided the ceiling was catastrophic. The argument i kept making, and kept struggling to land, was that the threat required a specific set of conditions to materialize and that most of those conditions weren't present in realistic attack scenarios.

What I didn't have then was a number. Now there is one. It doesn't prove the risk is zero. It does suggest the ceiling is significantly lower than the threat narrative assumed, and it validates the instinct that the response was outpacing the evidence.

I also kept saying that burning credibility on a threat model nobody had stress-tested would make the next serious conversation harder. That concern hasn't gone away.

## What Remains True

Stenberg is careful not to dismiss AI vulnerability research entirely, and he's right not to. He says clearly that modern AI analyzers substantially outperform traditional static analysis tools. The roughly twenty bugs documented in the curl analysis have real value even if none rose to CVE level.

There's also something instructive in what Mythos didn't find: zero memory-safety vulnerabilities. Stenberg observes that AI tools seem to excel at catching mismatches between code and documentation rather than the class of deep memory-corruption bugs that drive critical CVEs. That's a more honest picture of the capability than anything in the launch coverage, and it matters for anyone trying to figure out where to actually deploy these tools.

## The Credibility Problem

What i'm still thinking about this afternoon isn't the curl result itself. It's what the hype cycle cost.

The next time someone raises a serious concern about AI-assisted exploitation, the reeflex in a lot of rooms will be to recall how Mythos was framed. The people who were loudest about it being "dangerously good" don't get to walk that back cleanly. That credibility doesn't restore itself.

*The views expressed here are my own and do not represent my employer's official position.*
