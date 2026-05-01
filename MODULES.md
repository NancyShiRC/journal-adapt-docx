# Module Specifications

**Project:** Journal-Adaptive Academic Writing Workflow  
**For:** Codex (developer implementation reference)  
**Date:** 2026-05-01

Each module is defined by: inputs, outputs, constraints, human gate, and implementation notes.

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

## Module E — Three-Round Manuscript Revision

**Owner:** AI (Claude), paragraph-level human approval  
**Location:** `04_manuscripts/[PAPER_SLUG]/`

### Round 1: Diagnosis

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
