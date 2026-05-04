---
layout: post
title:  "The SBOM Illusion: Why Listing Your Software Components Isn't the Same as Securing Them"
date:   2026-05-04 09:00:00 -0400
categories: SBOM
tags: SBOM
---

*I've spent more time than i'd like staring at SBOM outputs that were supposed to answer basic supply chain questions and didn't.*

## What Is an SBOM?

A Software Bill of Materials is an inventory of the components, libraries, and dependencies that make up a piece of software. The nutrition label analogy gets used a lot. You can't manage what you can't see, and for a long time software supply chains have operated with almost no visibility into what's actually in them. An SBOM is supposed to fix that.

After SolarWinds, after Log4Shell, and after Executive Order 14028 mandated SBOM delivery for federal software procurement, the concept became policy. The security community mostly cheeered, which is understandable. Visibility into software composition is a real need. The problem is what got lost in translation: SBOMs became conflated with security when what they actually provide is a list.

## The Promise That Got Us Here

Log4Shell is the clearest reason SBOMs gained momentum as fast as they did. When the vulnerability dropped, the first question organizations needed to answer was whether they used Log4j at all, and if so, where. Most couldn't answer it in hours. A lot couldn't answer it in days. That's a genuine organizational failure, and SBOMs address it directly.

If every software artifact ships with a machine-readable inventory of its components, a security team can query that inventory when a new CVE drops and know their exposure immediately. That's useful. That's the real case for SBOMs and it's a solid one.

What happened instead is that this useful, narrow capability got inflated into a supply chain security strategy. Policy mandates and procurement requirements drove adoption withouut anyone doing the harder work of defining what an SBOM actually needs to look like to be useful when it counts.

## What the Tools Actually Produce

The most fundamental problem is that most SBOMs are incomplete, and the organizations relying on them don't know by how much.

A typical generation tool scans a repository or build artifact and enumerates direct dependencies. Modern software doesn't look like that. Applications pull in transitive dependencies that the tool may not fully resolve. They load plugins at runtime. They bundle vendored code that doesn't show up in any manifest. They call external services sitting three dependency layers deep.

A [comparative review](https://www.deepbits.com/blog/BreakingDownTheAccuracyOfSBOMGenerators) testing Trivy, Syft, Microsoft SBOM Tool, and GitHub Dependency Graph found that three of the four fail to resolve transitive dependencies at all, and all four have significant gaps parsing common manifest formats. A [separate analysis](https://www.endorlabs.com/learn/how-to-quickly-measure-sbom-accuracy-for-free) against a known set of 105 dependencies found missed components, malformed package identifiers, and incorrect version strings across tools. These aren't edge cases. They're what the current generation of tooling produces by default.

The harder issue is that incompleteness is invisible from the outside. You don't get a warning that your SBOM missed forty transitive dependencies. You get an SBOM that looks complete because it has entries in it.

## SBOMs Go Stale Fast

Even if you had a complete SBOM, it's only accurate at the moment it was generated.

Dependencies get updated. Build pipelines introduce components that weren't in the development environment. Container base images get pulled from registries that have changed since the SBOM was produced. In any environment with real release velocity, an SBOM from last week may not reflect what's running today.

What actually happens in most organizations is that SBOMs get generated once, delivered as a compliance artifact, and never touched again. It's the same failure mode as firewall rules that accumulate for years without review. You end up with a document that describes a system that no longer exists, and it carries an authority it hasn't earned. A stale SBOM doesn't just fail to help. It actively misleads you about your exposure.

## The SBOM Doesn't Prove Anything About the Software

Here's the problem that gets talked about least: even if your SBOM is complete and current, it doesn't verify anything about the software you're actually running.

SBOMs are documents. A supplier can generate one against source code and ship a binary built from different source. Someone with access to a build pipeline can swap a component after the SBOM is signed. A vendor can make an honest mistake and omit a dependency added in the final days of a release cycle. None of that shows up in the document.

Closing this gap requires reproducible builds, signed artifacts, and attestation frameworks with real verification on the consumer side. Most organizations have none of that in place. So what they have is a trusted document about an artifact they haven't actually verified. That's a meaningful distinction, and it's largely absent from the policy conversations driving SBOM adoption.

## The CVE Matching Problem

Say you have a complete, current SBOM tied to a verified artifact. You still have to figure out what to do with it.

The standard workflow feeds the SBOM into a vulnerability scanner, which correlates component identifiers against CVE databases and flags known-vulnerable components. In practice this is messier than it sounds. The same library can appear under different identifiers across different SBOM generators: CPE, PURL, package name, with no clean mapping between them. CVE coverage is uneven; many vulnerabilities in open source components go unregistered or get registered months after active exploitation. A [2025 empirical study](https://arxiv.org/abs/2511.20313) found that downstream vulnerability scanners produce a 92% false positive rate when applied to SBOM data, mostly because scanners flag vulnerabilities in code paths that are never actually reachable.

Teams learn to tune these alerts out. When you tune out noise at that volume, you end up tuning out real findings too.

## Where I Actually Land on This

SBOMs are worth having. The visibility problem they address is real, and organizations that can't answer "do we use this library" within minutes of a critical CVE dropping have a genuine gap. I'm not arguing against SBOMs.

What I'm arguing against is treating them as a supply chain security strategy.

The hard parts of supply chain security aren't listing your components. They're verifying that the software you're running matches what was built, detecting when something in the build process was tampered with, and having incident response procedures that are actually tested against supply chain scenarios rather than just endpoint compromises. An SBOM is one input into that work. It doesn't replace it.

SolarWinds is instructive here. The attacker's goal was to make a malicious component indistinguishable from the legitimate one. An SBOM generated from that compromised build pipeline would have documented the compromise faithfully, labeled correctly, with all the right metadata. The document wouldn't have told you anything was wrong.

## What Actually Matters

Reproducible build infrastructure. Binary transparency logs. Signing and attestation with real consumer-side verification. Threat modeling that treats build pipelines as attack surface. Incident response exercises run against supply chain scenarios specifically, not just endpoint compromises.

None of that is easy to mandate in a procurement requirement. That's partly why we ended up here. The SBOM requirement was achievable, so it happened. The deeper work is slower and more expensive and doesn't fit neatly into a checkbox.

The risk is that organizations invest heavily in SBOM generation, satisfy the compliance requirement, and remain fully exposed to the attacks that motivated the mandate. That's not a hypothetical failure mode. It's where the current trajectory leads if SBOM adoption stays disconnected from the verification and monitoring work it's supposed to support. The list is not the work.

*The views expressed here are my own and do not represent my employer's official position.*
