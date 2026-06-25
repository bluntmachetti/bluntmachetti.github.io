---
layout: post
title: "I Learn by Building"
date: 2026-06-25 12:00:00 +0000
description: "Why I use hackathons and public build logs as laboratories for AI-native resilience systems."
category: writing
log: "001"
read: "6 min"
summary: "Hackathons give me a deadline, a constraint, and a reason to turn an abstract idea into something testable. The outputs may look like separate projects — but they are all probes into the same question."
flags:
  - text: "personal"
    kind: ok
  - text: "methodology"
    kind: warn
---

I learn best by building.

Hackathons give me a deadline, a constraint, and a reason to turn an abstract idea into something testable. The outputs may look like separate projects — Aftershock, IncidentGym, Arena — but they are all probes into the same question: **how do we build trustworthy AI-native systems for resilience, security, and decision-making?**

## The projects

Aftershock explores how societies respond to disruption. It is a disaster-response simulation where a society of small AI agents must coordinate under pressure — triaging casualties, routing resources, and maintaining coherence when infrastructure fails. The headline finding: six small models out-deliver one big one at roughly 65% better lives-per-dollar, and written doctrine lifts protocol conformance at statistically credible levels.

IncidentGym looks at how organisations rehearse cyber incidents and measure readiness. It is a training environment where incident responders practice under realistic conditions, with deterministic scoring that makes every run auditable and replayable. The goal is not to gamify incident response — it is to make readiness measurable.

Arena asks what happens when agentic organisations and economies begin to make decisions at scale. It is a laboratory for simulating multi-agent economies where agents negotiate, trade, form alliances, and fail — providing a testbed for governance mechanisms before they touch real systems.

## The common thread

The common thread is not the hackathon. The common thread is **simulation, scoring, replayability, and evidence**.

Every project shares a core architecture:

- **Deterministic environments** where scenarios can be replayed and compared
- **Scoring functions** that make outcomes measurable, not just observable
- **Multi-agent coordination** under constraints that mirror real organisational pressure
- **Evidence-first reporting** that distinguishes what worked from what merely looked good

These are small laboratories by design: constrained enough to build quickly, rigorous enough to test whether the underlying idea survives contact with reality.

## Why public

Building in public is not about marketing. It is about **accountability**.

When I publish a build log, I commit to showing the negative results alongside the wins. Aftershock's field log documents the lives-saved headline we had to walk back. IncidentGym's log records scoring functions that did not work before the ones that did. This honesty is the point: it is the only way to build systems that other people can trust.

## What comes next

The next phase moves from hackathon laboratories to enterprise-scale applications. The patterns I have developed in these public builds — deterministic simulation, auditable scoring, multi-agent coordination under pressure — are the same patterns that enterprise organisations need for operational resilience.

The builds continue. The questions get bigger. The laboratories get more rigorous.

> The best way to understand a system is to build it. The best way to trust a system is to break it in public and show what survived.
