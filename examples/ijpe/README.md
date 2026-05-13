# Example: International Journal of Production Economics (IJPE)

A complete Phase 1 run — from raw journal PDFs to a ready-to-use revision ruleset.

---

## Background

The manuscript this example is built around sits at the intersection of **battery ownership models**, **closed-loop supply chain design**, and **service contract theory**. Core keywords: Battery-as-a-Service (BaaS), battery swapping, battery lifecycle management, contract design, and closed-loop supply chains.

The target journal is the **International Journal of Production Economics (IJPE)** — one of the leading outlets for operations management and production economics research, with a focus on quantitative models, supply chain optimization, and industrial applications.

---

## What was collected

Eight published IJPE papers were selected to represent the writing conventions of the journal in this topic area. The corpus spans 2017–2025 and covers three overlapping clusters:

**Closed-loop supply chain (CLSC) game models** — method-relevant papers showing how IJPE frames Stackelberg games, decision structures, and equilibrium analysis:
- Genc & De Giovanni (2017) — trade-in pricing, two-period CLSC game
- Maiti & Giri (2017) — two-way product recovery, price and quality demand

**Electric vehicle battery supply chains** — topic-relevant papers showing how IJPE positions EV battery research:
- Gu, Ieromonachou & Zhou (2019) — EV supply chain, government subsidies, imperfect information
- Gu, Zhou, Huang, Shi & Ieromonachou (2021) — battery secondary use, CLSC perspective
- Khodoomi, Tosarkani & Li (2025) — sustainable battery lifecycle, cost-sharing contracts, carbon policy
- Yang, Ma, He, Long, Jia & Liu (2025) — two-stage stochastic CLSC model, sustainability and resilience

**Battery recycling systematic literature reviews** — showing how IJPE handles SLR structure and framing:
- Luo, Yang & Jiang (2025) — EV battery recycling antecedents and consequences
- Zhu, Hu & Yang (2025) — circular supply chains for retired EV batteries

---

## What was done

**Step 1 — PDF conversion.** All 8 papers were converted from PDF to Markdown using MinerU (`mineru` CLI, per-paper mode). Converted files stored under `converted/` (not committed — raw corpus files are excluded from this repo).

**Step 2 — Per-paper Style Cards.** Each paper was read by Claude and summarized as a Style Card: structure, rhetorical moves, contribution framing, citation density, and formatting patterns — no copied text. Cards are in [`paper_style_cards/`](paper_style_cards/).

**Step 3 — Journal Style Card.** The 8 Style Cards were aggregated into a single [`journal_style_card.md`](journal_style_card.md). Each pattern is labeled STRONG (≥3 papers agree) or WEAK (1–2 papers). Extraction decisions are logged in [`style_extraction_log.md`](style_extraction_log.md).

**Step 4 — Writing Rules.** The Journal Style Card was converted into an actionable revision ruleset: [`writing_rules.md`](writing_rules.md). This is the file Phase 2 uses to revise a manuscript.

---

## Files in this folder

| File | What it is |
|------|-----------|
| `corpus_meta.yaml` | Paper list, relevance tags, conversion status |
| `paper_style_cards/` | 8 per-paper Style Cards |
| `journal_style_card.md` | Aggregated IJPE norms (STRONG / WEAK) |
| `style_extraction_log.md` | Phase 1 extraction log |
| `writing_rules.md` | Ready-to-use IJPE revision ruleset |

Raw PDFs and converted Markdown are not included (copyright).

---

## How to use this example

To skip Phase 1 for IJPE and go straight to revising your manuscript:

1. Point the skill to `examples/ijpe/writing_rules.md` when asked for an existing ruleset.
2. The skill will load these rules and proceed to Phase 2.

To run Phase 1 yourself on a different journal, use this folder as a reference for what the output should look like.
