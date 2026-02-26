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
LAYER 3: EXECUTION ─────────► Executable plays + deliverables + operator checklist
                                    │
LAYER 4: LEARNING ENGINE ───► Outcome tracking updates signal scores
                                    │
                    ┌───────────────┘
                    ▼
              LAYER 1 (next cycle, sharper)
```

### Layer 1: Research

Input a domain. The system runs a 7-step decomposed research pipeline — company deep-dive, buyer ecosystem mapping, existential decision point analysis, second-layer market dynamics, signal design, source discovery and detection specs, and a synthesis merge that assembles everything into a scored intelligence brief. Each step produces an intermediate artifact that can be re-run independently.

The brief covers what the company sells, who actually buys it (with situational qualifiers — not just titles), signal stacks that combine multiple evidence types into conviction thresholds, and individually scored signal hypotheses with detection specs, timing windows, and decay rates.

Every signal is scored across five dimensions — volume, detectability, specificity, timing precision, and actionability — using a weighted composite. Signals below the cut threshold (2.5) are killed. What survives has been pressure-tested, not assumed.

Every claim is sourced. Claims that can't be sourced are marked as hypotheses with an `[H]` tag so operators know exactly where the research is solid and where it's speculative.

Where structured data sources exist (DOL enforcement databases, job posting APIs, Census data), the system fires live API queries during research to upgrade volume estimates from hypothesis to verified — replacing `[H]` with hard counts and timestamps.

### Layer 2: Validation (Optional)

When discovery call transcripts are available (15+), the system extracts structured intelligence per-call, synthesizes patterns across all calls, then reconciles what buyers actually said against the Layer 1 research. Signal scores get updated — some go up (validated), some get killed (contradicted by reality).

This is where the system corrects itself. Research is a hypothesis. Calls are evidence.

### Layer 3: Execution

Produces three things from the intelligence:

1. **Play designs** — Signal-triggered outbound plays with A/B messaging variants, each tied to a specific signal stack. Not templates. Executable specs.
2. **PVP deliverables** — Point-of-View Pieces (competitive audits, benchmarks, analyses) that give prospects value before asking for anything. Every claim in a PVP goes through a verification system: claims are classified by source tier (V1 = primary data, V2 = secondary, H = hypothesis) and freshness, there's a hard budget on unverified claims, and if the budget is exceeded the system stops and flags it rather than publishing something unreliable. A built-in self-grade system scores each PVP on quality criteria and argues the negative case before scoring to prevent inflation.
3. **Operator checklist** — The step-by-step build plan: data sourcing strategy by ICP type, enrichment configuration, sending infrastructure, production workflow, and QA protocol.

### Layer 4: Learning Engine

Tracks outcomes per touch — opens, replies, meetings, objections, deal progression. After enough data accumulates, the system analyzes what worked, updates signal scores, identifies winning message variants, and recommends which signals to kill or double down on.

Updated scores feed back into Layer 1 for the next research cycle. Winning messaging feeds into Layer 3 for the next play design. The system doesn't just run — it learns.

---

## What Makes This Different

**Claim verification, not claim generation.** Most AI systems generate confident-sounding text. GTM Alpha classifies every claim by how it was sourced (verified from primary data, verified from secondary sources, or hypothesized by the model) and how fresh that source is (static, dynamic, or attributed). PVP deliverables have a hard claim budget — too many unverified claims and the system refuses to produce the output. It stops instead of shipping something unreliable.

**Signal scoring, not gut feel.** Every signal hypothesis gets scored on five weighted dimensions. The composite score determines whether a signal makes it into the brief or gets killed. After outcomes are tracked, those scores get updated with real data. Over time, the system converges on which signals actually predict pipeline — not which ones sounded good in a brainstorm.

**Compound loop across engagements.** Patterns that work for one company transfer to the next. A signal archetype that converts for a construction SaaS vendor might apply to any vertical SaaS company selling to fragmented, low-tech industries. The pattern library grows with every engagement, making each new deployment faster and more accurate than the last.

**Operator and client outputs are separated.** Internal docs use system notation, hypothesis markers, and operator-level detail. Client-facing deliverables are clean — no module numbers, no contract references, no technical scaffolding. The system knows who's reading.

**Live data validation, not just web search.** The research pipeline includes a data source registry that maps signal claim types to validated API endpoints — DOL enforcement databases, job posting aggregators, Census data. When a structured source exists, the system fires the query during research and replaces estimates with verified counts. Signals that can't be validated keep their `[H]` markers so you always know what's proven and what's projected.

---

## Where It's Run

GTM Alpha has been deployed against real companies across seven verticals — not tested in a sandbox.

**Bobyard (AI construction estimating)** — Full intelligence brief with 10 signal hypotheses, signal validation deep dives with named companies and real job board data, and a structured data pipeline spec for government RFP monitoring. Sample outputs from this run are included in this repo.

**Wold Architects & Engineers** — Architecture and engineering firm. Full pipeline: intelligence brief, 3 signal-triggered plays, PVP for a target school district, and operator checklist. Cold start — no call data, no existing playbooks, no prior outbound infrastructure.

**TaxWire (fintech)** — Tax compliance infrastructure. Brief, play design, and operator checklist. Used to stress-test source-hardening during brief generation.

**Helpside (PEO/HR services)** — Regional PEO serving 800+ SMBs. Ran twice — once on v3, once on v4. The v3 run surfaced 52 specific feedback items that drove the current system architecture. Every major improvement traces back to something that broke or underperformed in this deployment.

**Okland Construction** — First live test of API-validated signal detection. DOL enforcement data and TheirStack job posting APIs were queried during the research pipeline, upgrading 2 of 8 signal volume estimates from hypothesis to verified with real counts and timestamps.

**Light Labs (food safety testing)** — First run with all four modules on v4. 3 plays produced, PVP for Naked Nutrition. Used as the regression test for the v3→v4 decomposition — structural scorecard passed 9/9, content regression identified vendor detail preservation as an open improvement. First GTM Alpha email sent to a real prospect (February 2026).

**CoverForce (insurance distribution infrastructure)** — First self-prospecting run — GTM Alpha used to prospect for its own clients. 8 signals designed across 3 pain points, 3 plays produced, PVP for a target insurance agency. Post-run retro identified 7 systemic patterns and 7 backlog improvements.

Each run made the next one faster and more reliable. The system now has 40 embedded outbound principles, a data source registry with live API connections, and a post-run retro process that captures patterns across engagements. Seven runs in, the compound loop is working — not in theory, but across real verticals.

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
