# GTM Alpha

Most outbound starts with a list and a template. GTM Alpha starts with a question:

**What observable evidence proves a prospect is experiencing the exact pain your product solves — before they've started shopping?**

The system takes a company domain as input and produces signal-based intelligence that tells you who to contact, why now, and what to say — with every claim sourced or flagged. It then tracks what actually works, updates its own assumptions, and gets sharper every cycle.

This repo walks through the architecture and includes sample outputs. The full system runs on Claude Code with 8 skill modules, 7 contract specs, and a learning engine that closes the loop.

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

## Sample Outputs

This repo includes two example outputs to demonstrate the depth and rigor of the system:

### [Intelligence Brief — Bobyard](examples/intelligence-brief-sample.md)

A full Layer 1 brief for Bobyard (AI-powered estimating for commercial landscape contractors). Includes:
- Value proposition analysis (real pain, not marketing language)
- Three buyer personas with situational qualifiers
- Three signal stacks with conviction thresholds
- Ten individually scored signal hypotheses with validation data, timing windows, and decay rates
- Competitive intelligence and strategic recommendations
- Honest confidence assessment (what's validated vs. what's speculative)

### [Signal Validation Deep Dive](examples/signal-validation-sample.md)

A single signal hypothesis taken to ground truth. Shows the validation methodology: specific named examples, volume quantification, macro data cross-reference, confidence assessment by finding, and the GTM implication derived from the evidence.

---

## System Stats

- **8 skill modules** across 4 layers
- **7 contract specifications** defining data schemas, scoring rules, and quality gates
- **5-dimension weighted signal scoring** with composite cut threshold
- **3-tier claim classification** (V1: primary source / V2: secondary source / H: hypothesis) × freshness (static / dynamic / attributed)
- **Claim budget enforcement** — PVP deliverables refuse to generate if unverified claim count exceeds threshold

---

## Who Built This

I'm a GTM engineer. I build outbound systems, automation, and AI-powered workflows — Clay, Claude Code, cold email infrastructure, data enrichment, lead generation.

GTM Alpha started because I kept seeing the same problem: every time I built outbound for a new company, I was starting from scratch. The research didn't transfer. The playbooks didn't compound. The things I learned about what actually works disappeared into Slack threads and Google Docs that nobody ever read again.

So I built a system where the research is structured, the outputs are executable, claims are verified instead of assumed, and outcomes feed back into the next cycle. It's not a tool — it's an operating system for outbound intelligence.

If you want to see it run, reach out.
