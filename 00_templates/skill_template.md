# Temporary SKILL.md Template

**Version:** 1.0  
**Usage:** Generated from Journal Style Card + base writing rules. One per journal per date.

---

## SKILL METADATA

```yaml
skill_type: journal-adaptive-writing
target_journal: [JOURNAL NAME]
target_sections: [abstract / introduction / methods / results / discussion / policy]
paper_type: [theory+simulation / empirical / model+calibration / mixed]
base_skill: econ_writing_base.md
generated_from: journal_style_card_[DATE].md
created_date: [DATE]
priority_version: 1
status: [active / superseded]
```

---

## PART 1 — PRIORITY RULES (Non-Negotiable)

These rules override everything else. Apply in order.

### Priority 1 — HARD PRESERVE (never touch)

The following elements must be preserved verbatim in all revisions:
- All `\cite{}` commands and citation keys
- All LaTeX math environments (`\begin{equation}`, `\begin{align}`, etc.)
- All variable names, notation, and mathematical symbols
- All numerical results, statistics, and quantitative claims
- All footnotes and their content
- All figure and table references (`\ref{}`, `\label{}`)
- All model names, dataset names, and proper nouns
- All author-defined terminology and concept names

### Priority 2 — STRONG FOLLOW (journal style)

Apply writing patterns from the Journal Style Card where signal is STRONG (≥3 papers).
When P2 conflicts with P3, P2 wins. Log the conflict in revision log.

### Priority 3 — DEFAULT APPLY (general rules)

Apply general economic writing rules from `econ_writing_base.md`.
Apply when: P2 has no guidance on a dimension, or P2 signal is WEAK.

### Priority 4 — ALWAYS REMOVE (anti-patterns)

Remove these regardless of other rules:
- AI-taste openers: "This paper explores...", "In this study, we...", "It is worth noting that..."
- Generic contributions: "contributes to the literature on X by..."
- Hollow transitions: "Furthermore", "Additionally", "Moreover" used without logical function
- Circular emphasis: "importantly", "notably", "significantly" without quantification
- Template conclusions: "Future research should...", "More work is needed on..."
- Redundant meta-commentary: "As mentioned above", "As we will show below"

---

## PART 2 — SECTION-SPECIFIC GUIDANCE

### Abstract

**Journal norm:** [fill from Journal Style Card — structure, length, tense, register]

**Guidance:**
- [specific instruction derived from journal style card]
- [specific instruction derived from journal style card]
- [flag weak signals: "SIGNAL-WEAK: only 2 papers use X pattern"]

**Do not:**
- [anti-patterns specific to this journal's abstract style]

---

### Introduction

**Journal norm:** [fill from Journal Style Card]

**Opening move:**
[describe the required/preferred hook type for this journal]

**Problem framing:**
[describe how to build urgency — phenomenon → consequence → gap, or other pattern]

**Gap statement:**
[where and how to state the gap]

**Contribution placement and format:**
[early/late, numbered/embedded, voice preference]

**Literature:**
[integrated vs standalone, how to position vs prior work]

**Roadmap:**
[explicit vs narrative vs absent]

**Do not:**
- [intro anti-patterns]

---

### Method / Model

**Journal norm:** [fill from Journal Style Card]

**Entry point:** [intuition first / formal first — and how]

**Exposition style:** [theorem-proof / walkthrough / etc.]

**Notation:** [density level and conventions]

**Verification:** [what type of formal or empirical check is expected]

**Do not:**
- [method anti-patterns]

---

### Results

**Journal norm:** [fill from Journal Style Card]

**Narration style:** [result → mechanism → implication, or other]

**Mechanism emphasis:** [required / optional / absent in this journal]

**Robustness:** [where to put it and how to frame it]

**Do not:**
- [results anti-patterns]

---

### Discussion

**Journal norm:** [fill from Journal Style Card]

**Function:** [what discussion must add beyond results in this journal]

**Scope:** [how far to extend claims]

**Policy language:** [register and specificity level]

**Do not:**
- [discussion anti-patterns]

---

### Policy Implications (if applicable)

**Journal norm:** [fill from Journal Style Card]

**Placement:** [where in the paper]

**Claim specificity:** [how specific vs general]

**Audience register:** [academic / policy-accessible]

---

## PART 3 — CONFLICT RESOLUTIONS

Explicit rules for known conflicts between journal norms and general rules.

| Dimension | General Rule | This Journal | Resolution | Signal |
|-----------|-------------|--------------|------------|--------|
| [e.g., Passive voice] | Avoid | Common in methods | Use passive in methods only | STRONG |
| [e.g., Contribution format] | Numbered list | Embedded prose | Use embedded prose | STRONG |
| [e.g., Hedging] | Minimize | Moderate | Minimize but allow in limitations | WEAK |

---

## PART 4 — SIGNAL-WEAK FLAGS

These guidance items are based on 1-2 papers only. Apply with caution; log when applied.

- [e.g., "SIGNAL-WEAK: Calibration section may be standalone — only 1 paper in corpus does this"]
- [e.g., "SIGNAL-WEAK: Roadmap paragraph at end of intro — only paper_002 uses this"]

When applying a weak-signal rule, note in revision log:
```
Applied rule: [rule name] — SIGNAL-WEAK — flagged for human review
```

---

## PART 5 — LANGUAGE REGISTER CALIBRATION

Based on the journal's language profile:

- **Voice:** [instruction, e.g., "Prefer active voice; passive acceptable in methods and results"]
- **Sentence length:** [instruction]
- **Hedging:** [specific guidance — when to use, when not to]
- **Mathematical prose:** [how to introduce and explain equations]
- **Transitions:** [preferred transition style for this journal]
- **Formality:** [calibration]

---

## PART 6 — QUICK REFERENCE CHECKLIST

Before submitting a revised section, verify:

```
□ All citations preserved verbatim
□ All equations and notation unchanged
□ No new empirical claims added
□ Contribution format matches journal preference
□ Hook type matches journal preference
□ Hedging level calibrated to journal norm
□ Anti-AI-taste pass completed
□ All signal-weak applications flagged in revision log
□ Conflict resolutions applied per Part 3 table
```
