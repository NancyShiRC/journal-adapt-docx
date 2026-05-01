# Journal-Adaptive Academic Writing Workflow

**Status:** MVP Design Phase  
**Owner:** Product/Arch design by Claude (PM role); Implementation by Codex  
**Last Updated:** 2026-05-01

---

## What This Is

A workflow system that adapts your academic manuscript's language and argumentation style to match a specific target journal — by learning from that journal's published papers.

This is **not** an auto-writer. It is a style-transfer and revision workflow grounded in corpus evidence.

**Core pipeline:**

```
target journal corpus
  → Paper Style Cards (per-paper style extraction)
  → Journal Style Card (aggregated journal norms)
  → Temporary SKILL.md (adaptive writing rule set)
  → 3-round manuscript revision
  → Revision Log + Reusable Rules
```

---

## Why This Exists

Existing academic writing skills (e.g., `econ-writing-skill`) are:
- Static and domain-general
- Not adapted to specific journals
- Not aware of interdisciplinary paper types

This system solves that by extracting journal-specific writing norms from actual corpus papers and generating a temporary adaptive skill for each target journal.

---

## Documents in This Repo

| File | Purpose |
|------|---------|
| `README.md` | This file. Project overview. |
| `ARCHITECTURE.md` | Full system architecture for developers |
| `MODULES.md` | Per-module input/output specs |
| `00_templates/paper_style_card_template.md` | Template: extract style from one paper |
| `00_templates/journal_style_card_template.md` | Template: aggregate journal norms |
| `00_templates/skill_template.md` | Template: generate adaptive SKILL.md |
| `00_templates/revision_log_template.md` | Template: record each revision decision |

---

## Folder Structure

```
期刊匹配writing-skills/
├── README.md                          ← start here
├── ARCHITECTURE.md                    ← system design
├── MODULES.md                         ← module specs
│
├── 00_templates/                      ← reusable templates (core deliverable)
│   ├── paper_style_card_template.md
│   ├── journal_style_card_template.md
│   ├── skill_template.md
│   └── revision_log_template.md
│
├── 01_corpus/                         ← journal corpus (per journal)
│   └── [JOURNAL_NAME]/
│       ├── raw/                       ← source paper text (.gitignored)
│       ├── paper_style_cards/         ← AI-extracted style cards
│       └── corpus_meta.yaml           ← paper list + tags
│
├── 02_journal_style/                  ← aggregated journal style
│   └── [JOURNAL_NAME]/
│       ├── journal_style_card.md
│       └── style_extraction_log.md
│
├── 03_skills/                         ← generated skills
│   ├── base/
│   │   └── econ_writing_base.md       ← general econ writing rules
│   └── [JOURNAL_NAME]/
│       └── SKILL_[JOURNAL]_[DATE].md
│
├── 04_manuscripts/                    ← active manuscript work
│   └── [PAPER_SLUG]/
│       ├── input/                     ← original sections (LaTeX or .txt)
│       ├── diagnosis/                 ← round 1 output
│       ├── revised/                   ← round 2 output
│       └── revision_log/              ← round 3 output
│
└── 05_workflow_skills/                ← distilled reusable skills
    ├── journal_corpus_extraction.md
    ├── style_card_aggregation.md
    └── revision_workflow.md
```

---

## MVP Scope

One journal. One manuscript. Manual corpus preparation. Claude Code execution.

**MVP success criteria:**
- Can extract Paper Style Cards from 5–8 journal papers without copying original text
- Can aggregate a Journal Style Card with strong/weak signal labeling
- Can generate a Temporary SKILL.md with explicit priority rules
- Can run 3-round revision on one manuscript section
- Can produce a Revision Log with reusability assessments

---

## For Codex (Developer Instructions)

Read in this order:
1. `README.md` (this file) — understand the goal
2. `ARCHITECTURE.md` — understand the system design and design decisions
3. `MODULES.md` — understand each module's I/O before implementing
4. `00_templates/` — implement against these templates exactly

Key constraints to never violate:
- Paper Style Cards must never contain copied or paraphrased original text
- Revision output must never add new facts, data, or citations not in the original
- All LaTeX commands, citation keys, and equations must be preserved verbatim
- Priority order: Preserve facts > Journal style > General rules > Anti-AI-taste
