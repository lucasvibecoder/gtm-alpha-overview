# GTM Alpha

Most outbound starts with a list and a template. GTM Alpha starts with a question:

**What observable evidence proves a prospect is experiencing the exact pain your product solves — before they've started shopping?**

The system takes a company domain as input and produces signal-based intelligence that tells you who to contact, why now, and what to say — with every claim sourced or flagged. It then tracks what actually works, updates its own assumptions, and gets sharper every cycle.

This repo walks through the architecture and includes sample outputs.

---

## The Problem

B2B outbound research is mostly guesswork dressed up as strategy:

- **Unsourced confidence.** Briefs full of numbers with no methodology. "TAM is $4.2B" — according to who? Based on what?
- **Persona fiction.** Buyer profiles built from job titles, not from what actually triggers a purchase.
- **One-shot research.** A rep researches an account, sends emails, and never captures what they learned. The next rep starts from zero.
- **Signal blindness.** "They raised a Series B" is not a signal. A signal is observable evidence, connected to a specific pain, with a timing window that tells you when to reach out.

GTM Alpha replaces this with a system that compounds.

---

## Architecture

Four layers. Each feeds the next.

```
LAYER 1: RESEARCH ──────────► Intelligence brief with scored signals
                                    │
LAYER 2: VALIDATION ────────► Call data validates the research (optional)
                                    │
LAYER 3: EXECUTION ─────────► Executable plays + deliverables + operator blueprint
                                    │
LAYER 4: LEARNING ENGINE ───► Outcome tracking updates signal scores
                                    │
                    ┌───────────────┘
                    ▼
              LAYER 1 (next cycle, sharper)
```

### Layer 1: Research

Input a domain. The system produces a deep intelligence brief: what the company sells, who actually buys it (with situational qualifiers — not just titles), signal stacks that combine multiple evidence types into conviction thresholds, and individually scored signal hypotheses with detection specs, timing windows, and decay rates.

Every signal is scored across five dimensions — volume, detectability, specificity, timing precision, and actionability — using a weighted composite. Signals below the cut threshold are killed. What survives has been pressure-tested, not assumed.

Every claim is sourced. Claims that can't be sourced are marked as hypotheses with an `[H]` tag so operators know exactly where the research is solid and where it's speculative.

### Layer 2: Validation (Optional)

When discovery call transcripts are available (15+), the system extracts structured intelligence per-call, synthesizes patterns across all calls, then reconciles what buyers actually said against the Layer 1 research. Signal scores get updated — some go up (validated), some get killed (contradicted by reality).

This is where the system corrects itself. Research is a hypothesis. Calls are evidence.

### Layer 3: Execution

Produces three things from the intelligence:

1. **Play designs** — Signal-triggered outbound plays with A/B messaging variants, each tied to a specific signal stack. Not templates. Executable specs.
2. **PVP deliverables** — Point-of-View Pieces (competitive audits, benchmarks, analyses) that give prospects value before asking for anything. Every claim in a PVP goes through a verification system: claims are classified by source tier and freshness, there's a hard budget on unverified claims, and if the budget is exceeded the system stops and flags it rather than publishing something unreliable.
3. **Operator blueprint** — The step-by-step build plan: data sourcing strategy by ICP type, enrichment configuration, sending infrastructure, production workflow, QA protocol, and a weekly operating rhythm.

### Layer 4: Learning Engine

Tracks outcomes per touch — opens, replies, meetings, objections, deal progression. After enough data accumulates, the system analyzes what worked, updates signal scores, identifies winning message variants, and recommends which signals to kill or double down on.

Updated scores feed back into Layer 1 for the next research cycle. Winning messaging feeds into Layer 3 for the next play design. The system doesn't just run — it learns.

---

## What Makes This Different

**Claim verification, not claim generation.** Most AI systems generate confident-sounding text. GTM Alpha classifies every claim by how it was sourced (verified from primary data, verified from secondary sources, or hypothesized by the model) and how fresh that source is (static, dynamic, or attributed). PVP deliverables have a hard claim budget — too many unverified claims and the system refuses to produce the output. It stops instead of shipping something unreliable.

**Signal scoring, not gut feel.** Every signal hypothesis gets scored on five weighted dimensions. The composite score determines whether a signal makes it into the brief or gets killed. After outcomes are tracked, those scores get updated with real data. Over time, the system converges on which signals actually predict pipeline — not which ones sounded good in a brainstorm.

**Compound loop across engagements.** Patterns that work for one company transfer to the next. A signal archetype that converts for a construction SaaS vendor might apply to any vertical SaaS company selling to fragmented, low-tech industries. The pattern library grows with every engagement, making each new deployment faster and more accurate than the last.

**Operator and client outputs are separated.** Internal docs use system notation, hypothesis markers, and operator-level detail. Client-facing deliverables are clean — no module numbers, no contract references, no technical scaffolding. The system knows who's reading.

---

## Where It's Run

GTM Alpha has been deployed against real companies, not just tested in a sandbox.

**Wold Architects & Engineers** — Architecture and engineering firm acquired by a PE-backed holding company. Ran the full Fast Path: intelligence brief, play design with 3 signal-triggered outbound plays, PVP deliverables for a target school district, and a complete operator blueprint. Deliverables were reviewed by the growth engineering team and used to shape the outbound motion for the architecture vertical. This was a cold start — no call data, no existing playbooks, no prior outbound infrastructure.

**Helpsite (HR services)** — Ran as a live stress test of the v3 system. Produced the full brief and execution stack. The run surfaced 52 specific feedback items that drove the current version — claim sourcing gaps, document structure problems, and places where the system was too confident without evidence. Every major improvement in the current system traces back to something that broke or underperformed in this deployment.

**Bobyard (AI construction estimating)** — Full intelligence brief with 10 signal hypotheses, signal validation deep dives with named companies and real job board data, and a structured data pipeline spec for government RFP monitoring. Sample outputs from this run are included in this repo.

Each run made the next one faster. The Wold deployment took less iteration than Helpsite because the feedback loop had already tightened the output templates, claim verification rules, and scoring methodology. That's the compound loop working — not in theory, but across real engagements.

---

## Sample Outputs

### [Intelligence Brief — Bobyard](examples/intelligence-brief-sample.md)

Full Layer 1 brief: value prop analysis, buyer personas with situational qualifiers, signal stacks with conviction thresholds, 10 scored signal hypotheses with validation data and timing windows, competitive intelligence, and an honest confidence assessment separating what's validated from what's speculative.

### [Signal Validation Deep Dive](examples/signal-validation-sample.md)

A single signal hypothesis taken to ground truth — specific named companies, salary data, volume quantification, BLS cross-reference, and confidence ratings by finding. This is how every signal in every brief gets pressure-tested.

---

## Who Built This

I'm a GTM engineer. I build outbound systems, data enrichment pipelines, and AI-powered workflows — Clay, Claude Code, cold email infrastructure, lead generation.

I built GTM Alpha because the work kept disappearing. Every new company meant starting from zero — re-researching the same buyer patterns, re-learning which signals actually predict pipeline, re-building playbooks that someone at the last company already figured out. The research never transferred. The playbooks never compounded.

Now they do. The system structures the research so it's reusable, verifies claims instead of assuming them, scores signals so you know what to bet on, and tracks outcomes so the next cycle starts sharper than the last. Each deployment makes the next one faster — not because the tooling improves, but because the knowledge compounds.

If you want to see it run, reach out.
