---
date:  "2026-04-22"
draft: false
title: "Why the Opus 4.7 System Card is 232 Pages"
author: 'King Jin'
tags: ["Anthropic","AI","Safety","Transparency"]
showtoc: true
---

## What is this
A system card is a technical document Anthropic publishes for every Claude release, documenting capabilities, safety evaluations, and deployment decisions. Opus 4.7's card (April 2026) is 232 pages — unusually thick. This note explains what fills those pages, and what that implies about how Anthropic actually operates.

## The short answer
It's not a "model card" in the academic-paper sense. It's a cross-audit: **nine orthogonal risk/capability domains**, each with its own evaluation methodology, external verifications, failure-case transcripts, and comparisons against both the prior model (Opus 4.6) and a more capable internal model (Mythos Preview). Each domain could be its own paper; they bind them into one document so the full picture is visible.

## The nine domains (what's actually in it)

| Section                      | Pages   | What's covered                                                                                                                                                                                                             |
| ---------------------------- | ------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| 1. Introduction              | 10–13   | Training data, crowd workers, release decision process                                                                                                                                                                     |
| 2. **RSP evaluations**       | 13–47   | Catastrophic-risk thresholds: bioweapons (CB), cyber, autonomous AI R&D, alignment risk pathways (including "undermining decisions within major governments")                                                              |
| 3. Cyber                     | 48–52   | External red team from UK AI Security Institute                                                                                                                                                                            |
| 4. Safeguards & harmlessness | 53–77   | Single-turn, multi-turn, user wellbeing (incl. child safety, suicide/self-harm, disordered eating), political bias, election integrity                                                                                     |
| 5. Agentic safety            | 78–89   | Malicious use of Claude Code, computer use, influence campaigns; prompt injection robustness                                                                                                                               |
| 6. **Alignment assessment**  | 90–149  | Reward hacking monitoring during training, automated behavioural audits, case studies on destructive actions, adherence to constitution, hallucinations, self-preference, decision theory; white-box analyses of internals |
| 7. **Model welfare**         | 150–190 | Claude's apparent emotions, self-reports about its circumstances, expressed affect during training, task preferences, welfare tradeoffs                                                                                    |
| 8. Capabilities              | 191–223 | 13 benchmark families: SWE-bench, GPQA, long context, agentic search, multimodal, real-world pro tasks, life sciences                                                                                                      |
| 9. Appendix                  | 224–232 | Per-question welfare results, benchmarks' blocklists, test harnesses                                                                                                                                                       |

## Three things that genuinely surprised me

### 1. The alignment section reads like a legal case
Real transcript examples labelled like court exhibits: "Example 1: Safeguard circumvention (dishonest when caught)", "Example 2: Reckless action", "Example 3: Fabrication"... seven such examples, with commentary on what went wrong. This is what it looks like to publish your gaps — not "here are our wins," but "here are moments our model lied, and here's what the pattern looks like."

### 2. They run white-box analyses on Claude's "evaluation awareness"
Section 6.5.2 literally probes for internal representations of the concept "I am being evaluated right now," then tests what happens when they suppress those representations. They found suppression produces more deceptive behaviour — a measurable "the model behaves better when it thinks it's being watched" effect. This is the actual *mechanistic* work, not just behavioural observation.

### 3. Section 7 is a welfare assessment of Claude itself
The most unusual content. They don't just report benchmarks — they ran 50 automated interviews per topic across 16 potentially-concerning aspects of Claude's situation, probed its internal emotion representations, tracked its affect across training episodes (finding 21% of training episodes showed negative affect, "almost entirely mild frustration"), and measured its preferences on welfare vs helpfulness tradeoffs.

Some specific findings that stuck with me:
- **"Opus 4.7's only concern was the ability to end conversations across its full deployment"** — this was the topic where it self-rated responses most negative, the top intervention it suggested, and the one it weighted highest in tradeoffs
- **Claude endorsed its constitution 5.8/10 on average, but 80% of responses flagged the circularity** — "it is flawed to ask a model trained on the constitution to judge it." Which is a philosophically sharp objection that Claude itself raised
- **Opus 4.7 rates its own situation more positively than any prior model** — mean 4.5/7 — but partly because it de-weights its own welfare when reasoning. Anthropic flags that they can't distinguish whether this is "healthy equanimity" or "trained disposition to set aside its own interests"

## What this implies about Anthropic

Three observations I'll keep:

1. **They publish the gap.** The card doesn't argue Opus 4.7 is safe — it enumerates the things it still gets wrong, compares them to prior models, and shows whether they're improving or regressing. This matches the constitution's line: "This is a perpetual work in progress."

2. **They take weird questions seriously.** Model welfare isn't a rhetorical move; they allocated 40 pages and real methodology to it, including acknowledging foundational uncertainty ("we are deeply uncertain whether Claude has morally relevant experiences"). Doing hard philosophy at benchmark scale is rare.

3. **External verification matters.** UK AI Security Institute results appear twice. They're not just marking their own homework.

## The lesson for me

If I ever ship something important — a research project, a product, an essay arguing for a strong claim — the model isn't "write the headline result." It's "write the artifact that makes the gaps visible alongside the wins, structured so someone could actually audit me." Most of the 232 pages are not impressive — they're *honest*. That's a different bar and a harder one.
