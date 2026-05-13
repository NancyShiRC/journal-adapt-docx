# System Architecture

**Project:** Journal-Adaptive Academic Writing Workflow  
**Version:** 1.1 (post-MVP performance update)  
**Date:** 2026-05-01

---

## 1. Three-Layer Architecture

```
┌─────────────────────────────────────────────────────────┐
│  LAYER 1: CORPUS LAYER                                   │
│  Input: Target journal papers (PDF/text, human-selected) │
│  Output: Paper Style Cards (structured, no copied text)  │
└─────────────────────┬───────────────────────────────────┘
                      │
┌─────────────────────▼───────────────────────────────────┐
│  LAYER 2: STYLE LAYER                                    │
│  Input: Paper Style Cards                                │
│  Output: Journal Style Card → Temporary SKILL.md         │
└─────────────────────┬───────────────────────────────────┘
                      │
┌─────────────────────▼───────────────────────────────────┐
│  LAYER 3: REVISION LAYER                                 │
│  Input: SKILL.md + Author's manuscript                   │
│  Output: Diagnosis → Revised text → Revision Log         │
└─────────────────────────────────────────────────────────┘
```

These three layers are independent. Each can be replaced or upgraded without breaking the others.

---

## 2. Full Data Flow

Two distinct phases. Phase 1 runs once per journal. Phase 2 runs per manuscript section.

```
══════════════════════════════════════════════
PHASE 1 — CORPUS ANALYSIS  (runs once per journal, results cached)
══════════════════════════════════════════════

[Human] selects papers → corpus_meta.yaml
              │
[Module 0] Per-PDF conversion via MinerU (one file at a time)
              │
[Module A] corpus_meta.yaml finalized
              │
[Module B] Paper Style Card extraction — one card per paper
              │  (no copied text; structural/rhetorical descriptions only)
[Human] reviews cards
              │
[Module C] Journal Style Card aggregation
              │  (STRONG ≥3 papers, WEAK 1-2)
[Human] deep-reviews, fills Section 10
              │
[Module D] Temporary SKILL.md generated
              │  (covers ALL sections: 2A–2G)
[Human] confirms SKILL.md, sets status: active
              │
              ▼
        SKILL.md is now the only artifact
        needed for Phase 2. Corpus files
        are not read again during revision.

══════════════════════════════════════════════
PHASE 2 — MANUSCRIPT REVISION  (per session, loads SKILL.md only)
══════════════════════════════════════════════

[Module E0] Section Triage — read full paper ONCE
              │  Output: triage_report.md with priority and mode per section
[Human] approves triage, overrides priorities if needed
              │
              ├── HIGH sections (Abstract, Introduction)
              │     → Mode A: Full 3-round
              │        Round 1: Diagnosis
              │        [Human] approves
              │        Round 2: Revision
              │        [Human] accepts/rejects paragraph-by-paragraph
              │        Round 3: Revision Log + reusability assessment
              │        [Human] marks rule candidates
              │
              ├── MED sections (Lit Review, Methods, Discussion)
              │     → Mode B: Merged Round
              │        Diagnosis + revision in one output
              │        Simplified log (rule candidates only)
              │        [Human] accepts/rejects
              │
              └── LOW sections (Results, Conclusion)
                    → Mode C: Fast Scan
                       Flags HIGH severity issues only
                       No revision unless author requests

              ▼
[Module F] Rule candidates → 05_workflow_skills/
```

---

## 3. Human vs AI Responsibility Matrix

| Step | Owner | Human Gate Type |
|------|-------|----------------|
| Select corpus papers | **Human** | Decision (AI cannot select) |
| Tag paper relevance in corpus_meta.yaml | **Human** | Decision |
| Extract Paper Style Cards | AI | Review: verify no original text copied |
| Aggregate Journal Style Card | AI | Review: confirm signal strength labels |
| Generate SKILL.md | AI | Confirm: check priority rules are correct |
| Round 1 Diagnosis | AI | Approve before proceeding to Round 2 |
| Round 2 Revision | AI | Accept/reject each paragraph |
| Round 3 Revision Log | AI | Mark reusable rules |
| Distill workflow skill | Human-led + AI draft | Decision |

**Rule:** No AI output advances to the next step without human confirmation.

---

## 4. Priority System (embedded in every SKILL.md)

```
Priority 1 — HARD PRESERVE
  All facts, data, model results, citations, LaTeX commands,
  equations, variable names, footnotes. Never touch these.

Priority 2 — STRONG FOLLOW
  Writing patterns extracted from target journal corpus
  (strong signal only: ≥3 papers in agreement).

Priority 3 — DEFAULT APPLY
  General economic/academic writing rules
  (from econ_writing_base.md).

Priority 4 — ALWAYS REMOVE
  AI-taste phrases, generic templates, filler transitions,
  hollow contribution statements, overused hedging.
```

**Conflict resolution:**
- P2 beats P3 always (journal-specific beats general)
- When P2 signal is weak (1-2 papers), fallback to P3, flag as "signal weak"
- All conflicts resolved by P2>P3 must be logged in revision log

---

## 5. Anti-Plagiarism Design

The Paper Style Card extraction is the key risk point. The system enforces:

**Allowed outputs from AI when reading corpus papers:**
- Abstract structural descriptions: "3-sentence structure: phenomenon → gap → method"
- Language style tags: "active voice dominant, technical register, low hedging"
- Rhetorical move descriptions: "contribution stated as numbered list, 'we show X' format"
- Statistical patterns: "80% of intros open with a policy-relevant statistic"
- Section architecture patterns: "literature review embedded in intro, not standalone"

**Prohibited outputs:**
- Any direct quote from corpus paper
- Any paraphrase of corpus paper sentence
- Any sentence where the original source paper can be identified

**Implementation:** The Paper Style Card template explicitly states these rules at the top, and the AI must acknowledge them before extraction begins. Human reviewer checks all cards for any text that reads like paraphrase.

---

## 6. Journal Norms vs General Writing Rules

```
                    Journal Style Card
                          │
              ┌───────────┴────────────┐
         STRONG signal            WEAK signal
         (≥3 papers agree)        (1-2 papers)
              │                        │
    Journal preference wins    Fallback to general rules
              │                        │
         Log conflict             Label "signal-weak"
```

**Conflict Table Example (included in every Journal Style Card):**

| Dimension | General Rule | This Journal | Winner | Signal |
|-----------|-------------|--------------|--------|--------|
| Passive voice | Avoid | Common in methods | Journal | STRONG |
| Contribution format | Numbered list | Embedded prose | Journal | STRONG |
| Hedging | Minimize | Moderate use | Tie | WEAK |
| Discussion scope | Stay narrow | Policy reach | Journal | STRONG |

---

## 7. Performance Design

### The Two-Phase Rule (critical for cost control)

Phase 1 (corpus analysis) runs **once per journal**. Phase 2 (revision) runs **per section, per session**. Never mix them.

The most common performance mistake: Codex re-reads corpus papers or the Journal Style Card during a revision session. Once SKILL.md is active, it is the only context source for revision. Corpus files are never loaded in Phase 2.

### Context size targets during Phase 2

| What gets loaded | Approx tokens | Notes |
|-----------------|--------------|-------|
| SKILL.md Part 1 (Priority Rules) | ~300 | Always |
| SKILL.md Part 2 (one section) | ~400–600 | Load only the block for the section being revised |
| SKILL.md Part 3–5 (conflicts, flags, register) | ~400 | Always |
| Section text (one section of manuscript) | ~800–2000 | The section being revised |
| **Total per revision call** | **~2000–3300** | Well within single-call context |

Do not load: Journal Style Card (~3000 tokens), corpus papers (~8000–20000 tokens each).

### Revision mode time targets

| Mode | LLM calls | Target wall time |
|------|-----------|-----------------|
| Mode A (3-round, HIGH sections) | 3 sequential + 2 human gates | 8–12 min |
| Mode B (merged, MED sections) | 1–2 calls + 1 human gate | 3–5 min |
| Mode C (fast scan, LOW sections) | 1 call | 1–2 min |

### Full-paper revision estimate (7 sections)

```
Section Triage (E0):        1 call    ≈ 3 min
Abstract (Mode A):          3 calls   ≈ 10 min
Introduction (Mode A):      3 calls   ≈ 10 min
Lit Review (Mode B):        2 calls   ≈ 4 min
Methods (Mode B):           2 calls   ≈ 4 min
Results (Mode C):           1 call    ≈ 2 min
Discussion (Mode B):        2 calls   ≈ 4 min
Conclusion (Mode C):        1 call    ≈ 2 min
─────────────────────────────────────────────
Total                       15 calls  ≈ 39 min
```

Compare to naive sequential 3-round on all sections: 7 × 3 calls × ~5 min = ~105 min.

### SKILL.md coverage requirement

SKILL.md must cover all sections (Parts 2A–2G) before full-paper revision begins. A SKILL.md with only `target_sections: ["introduction"]` cannot run full-paper revision — Codex will fall back to general rules for uncovered sections, losing all journal-specific signal.

---

## 9. Extensibility (MVP → Future)

| Dimension | MVP | Extension Path |
|-----------|-----|---------------|
| Corpus ingestion | Manual: paste text to `raw/` | API: Semantic Scholar, CrossRef, Unpaywall |
| Journal count | 1 | `01_corpus/[JOURNAL]/` structure supports N journals |
| SKILL versioning | Date-named files | Git tags on `03_skills/` |
| Revision execution | Conversational (Claude Code) | Batch via Claude API |
| Open source release | Local tool | `00_templates/` + `05_workflow_skills/` publishable immediately |

**Git hygiene for open source:**
```gitignore
# .gitignore
01_corpus/*/raw/          # copyright: never commit source papers
04_manuscripts/*/input/   # author's unpublished work
```

The `corpus_meta.yaml` files (metadata only) are safe to open-source.

---

## 10. Reference Projects

These were evaluated during design. None implement the full corpus→style→skill pipeline.

| Project | URL | What we borrowed |
|---------|-----|-----------------|
| econ-writing-skill | github.com/hanlulong/econ-writing-skill | Skill encoding structure, paper-type adaptation tables |
| academic-paper-skills | github.com/lishix520/academic-paper-skills | Style calibration from corpus, priority hierarchy concept |
| paper-writing-skill (SNL-UCSB) | github.com/SNL-UCSB/paper-writing-skill | Section-level rhetorical guidance structure |

**Key gap this project fills:** None of the above extract journal norms from a user-provided corpus. This is the novel contribution of this architecture.

---

## 11. MVP Timeline

```
Week 1:
  - Create folder structure
  - Write all 4 templates (00_templates/)
  - Human selects 5-8 target journal papers, exports text
  - AI extracts Paper Style Cards; human reviews

Week 2:
  - AI aggregates Journal Style Card; human deep-reviews
  - AI generates Temporary SKILL.md; human confirms
  - Run 3-round revision on one manuscript section

Week 3:
  - Complete Revision Log
  - Identify rules worth generalizing
  - Draft 05_workflow_skills/ entries
```
