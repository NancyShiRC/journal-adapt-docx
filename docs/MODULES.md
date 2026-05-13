# Module Specifications

**Project:** Journal-Adaptive Academic Writing Workflow  
**For:** Codex (developer implementation reference)  
**Date:** 2026-05-01

Each module is defined by: inputs, outputs, constraints, human gate, and implementation notes.

---

## Module 0 — Document Conversion Preprocessing

**Owner:** AI runs local tool; human supplies source files  
**Location:** `01_corpus/[JOURNAL_NAME]/converted/` and `04_manuscripts/[PAPER_SLUG]/converted/`

### Inputs
- Target journal PDFs in `01_corpus/[JOURNAL_NAME]/raw/`
- Manuscript PDF in `04_manuscripts/[PAPER_SLUG]/input/`
- Local PDF-to-Markdown converter, currently `mineru-pdf-md`

### Outputs
```text
converted/
  AGENT_README.md
  agent_readable.md
  [per-document Markdown/JSON/assets]
```

### Constraints
- Raw PDFs and converted full-text outputs must not be committed if they contain copyrighted papers or unpublished manuscript content.
- Conversion quality must be checked before style extraction or revision.
- If batch conversion fails or is slow, run per-PDF conversion and record the issue in the MVP test log.

### Human Gate
Human confirms that the correct source PDFs and manuscript were supplied. AI reports conversion failures and quality concerns before using the converted content.

### Implementation Notes
- Use converted Markdown as the default reading source for Modules B and E.
- For MVP testing, a partial converted corpus may be used only with explicit `WEAK` signal labels.

### MinerU Conversion Protocol (from MVP test 2026-05-01)

**Skill location:** `/Users/wantong.cai/.codex/skills/mineru-pdf-md/`  
**Wrapper script:** `~/.codex/skills/mineru-pdf-md/scripts/pdf_to_agent_md.py`  
**MinerU binary:** `/Users/wantong.cai/.local/share/codex-mineru/venv/bin/mineru`

**CRITICAL: Do NOT pass a directory to the wrapper for corpus batch conversion.**

Folder-mode triggers MinerU's internal HTTP server to process all PDFs in parallel batches. The server crashes mid-batch on macOS with `503 Service Unavailable` after completing the first batch only. This was observed in MVP: 8 PDFs submitted, 2 succeeded, 6 failed.

**Required approach — convert each PDF individually:**
```bash
# For each corpus PDF:
python3 ~/.codex/skills/mineru-pdf-md/scripts/pdf_to_agent_md.py \
  "01_corpus/[JOURNAL]/raw/paper.pdf" \
  --output-dir "01_corpus/[JOURNAL]/converted/paper_name"

# For the manuscript:
python3 ~/.codex/skills/mineru-pdf-md/scripts/pdf_to_agent_md.py \
  "04_manuscripts/[SLUG]/input/manuscript.pdf" \
  --output-dir "04_manuscripts/[SLUG]/converted/manuscript"
```

After all individual conversions complete, consolidate into a single `agent_readable.md`:
```bash
# Manually or via script: cat all per-PDF agent_readable.md files into one index
# Update AGENT_README.md to list all successfully converted files
```

**Conversion quality check before proceeding to Module B:**
- Verify `AGENT_README.md` shows exit code `0` for each PDF
- Spot-check one converted `.md` file — confirm math formulas render as LaTeX, tables are present, reading order is correct
- If a PDF fails after 2 retries, mark `converted: false` in `corpus_meta.yaml` and exclude from style extraction

---

## Module A — Corpus Setup

**Owner:** Human  
**Location:** `01_corpus/[JOURNAL_NAME]/`

### Inputs
- Target journal name
- Author's topic keywords (3–6 terms)
- Method type: `theory+simulation` | `empirical` | `model+calibration` | `qualitative` | `mixed`
- 5–8 paper texts (PDF exported to `.txt`, placed in `raw/`)

### Outputs
```yaml
# corpus_meta.yaml
journal: "Journal Name Here"
topic_keywords: ["keyword1", "keyword2", "keyword3"]
method_type: "theory+simulation"
papers:
  - id: paper_001
    authors: ["LastName1", "LastName2"]
    year: 2022
    title: "Full paper title"
    relevance: "topic+method"   # options: topic+method | topic | method | supplement
    file: raw/lastname2022.txt
    notes: "optional human notes"
```

### Constraints
- Minimum 3 papers to generate a Journal Style Card with any strong signals
- Recommended 5–8 papers for robust signal detection
- `relevance: "topic+method"` papers are weighted highest in aggregation

### Human Gate
Human decides which papers to include and assigns relevance tags. AI does not participate in paper selection.

---

## Module B — Paper Style Card Extraction

**Owner:** AI (Claude)  
**Location:** `01_corpus/[JOURNAL_NAME]/paper_style_cards/`

### Inputs
- Single paper text from `raw/`
- `00_templates/paper_style_card_template.md`
- `corpus_meta.yaml` (for paper ID and relevance tag)

### Outputs
- `paper_style_cards/paper_001_lastname2022.md` (one file per paper)

### Constraints — CRITICAL
```
PROHIBITED (causes rejection of card):
  - Any direct quote from the paper
  - Any sentence that reads as paraphrase of original
  - Reproducing any named result, statistic, or finding

REQUIRED:
  - All descriptions must be structural/rhetorical (how, not what)
  - Style tags must be categorical (active/passive, high/low, technical/policy)
  - Example patterns must describe the move, not reproduce content
```

### Human Gate
Human reviews every extracted card before proceeding. Checks:
1. No original text reproduced
2. Structural descriptions are accurate to the actual paper
3. Style tags are calibrated (not all "high technical" for every paper)

### Implementation Notes
- AI must receive the prohibition rules before reading each paper
- Run extraction one paper at a time, not in batch
- If paper is behind paywall and only abstract is available, mark `extraction_scope: abstract_only`

---

## Module C — Journal Style Card Aggregation

**Owner:** AI (Claude), with mandatory human deep-review  
**Location:** `02_journal_style/[JOURNAL_NAME]/`

### Inputs
- All Paper Style Cards from `01_corpus/[JOURNAL_NAME]/paper_style_cards/`
- `00_templates/journal_style_card_template.md`

### Outputs
- `journal_style_card.md`
- `style_extraction_log.md` (records which papers supported each claim)

### Signal Strength Rules
```
STRONG signal: pattern observed in ≥3 papers (or ≥60% of corpus)
WEAK signal:   pattern observed in 1-2 papers
ABSENT:        pattern explicitly not observed in any paper
```

Every claim in the Journal Style Card must be tagged with signal strength and paper IDs that support it.

Example:
```markdown
- Contribution stated as embedded prose (not numbered list) [STRONG: paper_001, paper_003, paper_005]
- Discussion section extends to policy implications [STRONG: paper_001, paper_002, paper_004, paper_006]
- Passive voice used in methods section [WEAK: paper_002, paper_003]
```

### Human Gate
Human must review and may:
- Downgrade STRONG → WEAK if they disagree with the pattern
- Add observations not captured by AI
- Complete the Conflict Table (Journal vs General rules)

### Implementation Notes
- The `style_extraction_log.md` must show evidence for every aggregated claim
- Contradictions across papers must be noted (not silently resolved)

---

## Module D — Temporary SKILL.md Generation

**Owner:** AI (Claude)  
**Location:** `03_skills/[JOURNAL_NAME]/`

### Inputs
- `02_journal_style/[JOURNAL_NAME]/journal_style_card.md`
- `03_skills/base/econ_writing_base.md`
- Author's paper type and target sections (from conversation)

### Outputs
- `SKILL_[JOURNAL]_[YYYYMMDD].md`

### Required Sections in Output SKILL.md
```
1. Priority Rules (hardcoded, non-negotiable)
2. Section-specific guidance per requested section
   (abstract / introduction / methods / results / discussion / policy implications)
3. Explicit conflict resolutions (journal vs general)
4. Do-not-do list (journal-specific anti-patterns)
5. Signal-weak flags (where evidence is thin)
```

### Human Gate
Human reviews SKILL.md and confirms:
- Priority rules are correct
- No guidance asks AI to add new content
- Conflict resolutions match human judgment
- Weak-signal items are flagged (not stated as facts)

---

## Module E0 — Section Triage (Full-Paper Fast Scan)

**Owner:** AI (Claude)  
**Location:** `04_manuscripts/[PAPER_SLUG]/diagnosis/`  
**When to run:** Before any per-section revision on a new manuscript, or when revising more than 2 sections in a single session.

### Purpose

Read the full manuscript once and produce a priority map. This avoids re-reading the full text for each section during Module E revision. It also lets the author decide which sections get full 3-round treatment vs. merged or fast-scan treatment before any token-intensive revision starts.

### Inputs
- Full manuscript text (converted Markdown from `converted/`)
- Active SKILL.md (Part 1 Priority Rules only — do NOT load section-specific guidance yet)

### Output: `diagnosis/triage_report.md`

```markdown
# Section Triage Report

date: [DATE]
manuscript: [PAPER_SLUG]
skill_used: [SKILL filename]

| Section | Paragraphs | Est. Match Score | Highest Severity | Priority | Recommended Mode |
|---------|-----------|-----------------|-----------------|----------|-----------------|
| Abstract | N | [1-5] | HIGH/MED/LOW | HIGH/MED/LOW | 3-round / merged / fast-scan |
| Introduction | N | [1-5] | ... | ... | ... |
| Literature Review | N | [1-5] | ... | ... | ... |
| Methods/Model | N | [1-5] | ... | ... | ... |
| Results | N | [1-5] | ... | ... | ... |
| Discussion | N | [1-5] | ... | ... | ... |
| Policy Implications | N | [1-5] | ... | ... | ... |
| Conclusion | N | [1-5] | ... | ... | ... |

## Top Problems by Section
[One paragraph per section: what are the 1-3 most important issues?
No paragraph-level detail. Enough for the author to approve or override priority.]
```

### Human Gate
Author reviews the triage report and may:
- Override priority (e.g., downgrade Results from MED to fast-scan)
- Reorder sections
- Exclude sections from this revision session

**No revision begins until triage is approved.**

### Why This Matters for Performance
Reading the full paper once in triage costs ~1 LLM call. Without triage, Module E reads each section separately, costing N calls just for loading. For a 7-section paper: triage saves ~6 redundant full-context reads.

---

## Module E — Manuscript Revision

**Owner:** AI (Claude), paragraph-level human approval  
**Location:** `04_manuscripts/[PAPER_SLUG]/`

### Session Entry Check (run before any revision)

```
IF SKILL_[JOURNAL]_[DATE].md exists AND status = active:
  → Load SKILL.md only. Do NOT re-read corpus papers, journal style card, or paper style cards.
  → Go directly to Module E0 (triage) or Module E (revision) as appropriate.

IF SKILL_[JOURNAL]_[DATE].md does not exist or is outdated:
  → Run Modules B → C → D first, then return here.
```

**This check is mandatory.** Corpus analysis (Modules B/C/D) runs once per journal, not once per revision session.

---

### Revision Modes

Each section is assigned one of three modes based on the triage report.

#### Mode A — Full 3-Round (for HIGH priority sections: Abstract, Introduction)

Full diagnostic round → human approval → revision round → human approval → revision log.  
Use when: journal match score ≤ 3, or highest severity = HIGH, or section is Abstract/Introduction.

#### Mode B — Merged Round (for MED priority sections: Literature Review, Methods, Discussion)

Diagnosis and revision combined in one output. Simplified log (rule candidates only, no full original/revised text).  
Use when: journal match score 3-4, highest severity = MED.

**Merged round output format:**
```markdown
## [Section Name] — Merged Revision

### Changes Made
| Paragraph | Problem | Change | Rule | Source |
|-----------|---------|--------|------|--------|
| Para N | [problem type + description] | [what changed] | [rule] | journal-card/econ-base |

### Unchanged Paragraphs
Paragraphs [list]: no issues above LOW severity.

### Rule Candidates
- [rule candidate 1]
- [rule candidate 2]
```

#### Mode C — Fast Scan (for LOW priority sections: Results, Conclusion)

Read section, output a short list of any HIGH severity issues only. No revision output unless author requests it.  
Use when: journal match score ≥ 4, no HIGH severity issues expected.

**Fast scan output format:**
```markdown
## [Section Name] — Fast Scan

Overall match: [score]/5
Issues above LOW severity: [none / list]
Recommendation: [no revision needed / one specific fix]
```

---

### Round 1: Diagnosis (Mode A only)

**Inputs:**
- Original manuscript section text (`input/[section].tex` or `.txt`)
- Active SKILL.md

**Output:** `diagnosis/[section]_diagnosis.md`

**Format per paragraph:**
```markdown
## Paragraph [N] — Lines [X]–[Y]

**Problems:**
- [STYLE] Description of style mismatch with journal norms
- [LOGIC] Description of logical gap or weak connection
- [AI-TASTE] Specific generic phrase or template sentence
- [JOURNAL-MISMATCH] How this departs from journal style card

**Applied rule:** [rule name from SKILL.md]
**Signal strength:** [STRONG / WEAK]
**Journal match score:** [1-5]
**Priority fix:** [STYLE / LOGIC / AI-TASTE / JOURNAL-MISMATCH]
```

**Human Gate:** Human approves diagnosis before Round 2 begins. May override any diagnosis.

---

### Round 2: Revision

**Inputs:**
- `input/[section].tex` (original)
- `diagnosis/[section]_diagnosis.md` (approved)
- Active SKILL.md

**Output:** `revised/[section]_v1.tex`

**Hard constraints (never violate):**
```
PRESERVE VERBATIM:
  - All \cite{} commands and citation keys
  - All LaTeX math environments (\begin{equation}...\end{equation})
  - All variable names and notation
  - All numerical results and statistics
  - All footnotes
  - All figure/table references (\ref{}, \label{})

DO NOT ADD:
  - New empirical claims
  - New citations
  - New model results
  - Interpretations not in the original

EACH CHANGE MUST BE LABELED:
  - % REVISED: [rule applied] [source: journal-card/econ-base/logic-fix]
```

**Human Gate:** Human accepts or rejects each revised paragraph individually. Rejected paragraphs revert to original or go back for re-revision.

---

### Round 3: Revision Log

**Inputs:**
- `input/[section].tex` (original)
- `revised/[section]_v1.tex` (accepted revision)
- Approved diagnosis

**Output:** `revision_log/[section]_log.md`

**Format per revision entry:**
```markdown
---
paragraph: [N]
section: [introduction]
revision_date: [DATE]
---

## Original Text
[paste original paragraph]

## Diagnosis
- Problem type: [STYLE / LOGIC / AI-TASTE / JOURNAL-MISMATCH]
- Issue: [specific description]
- Severity: [HIGH / MED / LOW]

## Revised Text
[paste accepted revision]

## Rationale
- Rule applied: [rule name]
- Source: [journal-card (STRONG) / journal-card (WEAK) / econ-base / logic-fix]
- Conflict resolved: [yes/no — if yes: journal won over general because X]

## Reusability Assessment
- Worth generalizing? [YES / NO / MAYBE]
- If YES:
  - Rule candidate: "[write the generalizable rule in one sentence]"
  - Target skill: [this-journal-only / journal-adaptive-general / econ-base]
  - Condition: [when does this rule apply]
```

**Human Gate:** Human marks which rules are worth generalizing. These feed into `05_workflow_skills/`.

---

## Module F — Workflow Skill Distillation

**Owner:** Human-led, AI assists with drafting  
**Location:** `05_workflow_skills/`

### Inputs
- All `revision_log/` entries where `Worth generalizing? YES`
- Completed Journal Style Cards (for pattern examples)

### Outputs
- `journal_corpus_extraction.md` — how to run Modules A + B
- `style_card_aggregation.md` — how to run Module C
- `revision_workflow.md` — how to run Module E (full 3-round process)

### Format
Each workflow skill is a standalone Claude Code skill file:
- Goal statement
- Step-by-step instructions
- Required inputs checklist
- Quality checks
- Example outputs

These are the final reusable artifacts. They should be written so any future user can run the workflow with a new journal and new manuscript.
