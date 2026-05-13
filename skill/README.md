# journal-adapt

A Claude Code skill that learns a target journal's writing conventions from its published papers, then revises your manuscript to match.

Not an auto-writer. A style-transfer revision tool grounded in corpus evidence.

---

## How it works

```
Your journal PDFs
  → PDF-to-Markdown conversion (MinerU)
  → Per-paper Style Cards (structure + rhetoric only, no copied text)
  → Journal Style Card (aggregated norms, STRONG/WEAK signal labels)
  → Journal Writing Rules (your revision ruleset)
  ↓
[You review and confirm the rules]
  ↓
Your manuscript
  → Diagnosis (per paragraph: problem type, severity, journal match score)
  → Revision (priority rules applied, no new facts added)
  → Revision Log (what changed, what rule, what was preserved)
  → Revised Markdown output
```

Phase 1 (corpus analysis) runs once per journal and produces a reusable ruleset. Phase 2 (revision) runs per manuscript.

---

## Prerequisites

**MinerU** — for PDF-to-Markdown conversion.

```bash
pip install mineru
mineru --version   # verify installation
```

Install guide: [github.com/opendatalab/MinerU](https://github.com/opendatalab/MinerU)

**Claude Code or Codex** with file read/write and Bash tool access.

---

## Installation

Copy the `skill/` folder to your Claude skills directory:

```bash
cp -r skill/ ~/.claude/skills/journal-adapt/
```

Verify:
```
~/.claude/skills/journal-adapt/
├── SKILL.md
└── base_rules/
    ├── economics.md
    ├── ml_cv_nlp.md
    ├── cs_engineering.md
    └── general_academic.md
```

---

## Usage

Invoke in Claude Code or Codex:

```
/journal-adapt
```

Or say: *"Help me revise my paper for [journal name]"* — Claude will recognize the intent and load the skill.

The skill will ask for:
1. Target journal name
2. Folder containing journal PDFs (5–8 papers recommended)
3. Your paper's discipline
4. Your manuscript file (PDF or Markdown)
5. Which sections to revise (or "full paper")

---

## Supported disciplines

Built-in base writing rules for:

| Discipline | Rules source |
|------------|-------------|
| Economics | `base_rules/economics.md` |
| ML / CV / NLP | `base_rules/ml_cv_nlp.md` |
| CS / Engineering | `base_rules/cs_engineering.md` |
| Other | Bring your own, or skip |

For disciplines not listed: the skill will ask if you have a writing rules file to use (any SKILL.md or plain-text guide works), or you can skip base rules and rely on journal-specific norms alone.

---

## Priority system

Every revision follows a strict priority order:

| Priority | What | Rule |
|----------|------|------|
| P1 | Hard preserve | Equations, citation keys, variable names, numerical results — never touched |
| P2 | Journal style | STRONG-signal patterns from your corpus (≥3 papers agree) |
| P3 | Discipline base rules | General writing norms for your field |
| P4 | Always remove | AI-taste phrases, hollow transitions, generic contribution statements |

P2 beats P3 when they conflict. All conflicts are logged.

---

## Output

Saved to `[manuscript_name]_revised/` next to your manuscript file:

```
[manuscript_name]_revised/
├── abstract_revised.md
├── introduction_revised.md
├── ...
├── [section]_revision_log.md    ← per-section: what changed and why
└── revision_summary.md          ← reusable rule candidates across all sections
```

Output is Markdown. Transfer to LaTeX or Word yourself, or pipe to another agent.

---

## Known limitations

- **MinerU required.** No MinerU, no PDF conversion. Markdown manuscripts work without it.
- **Table corruption.** MinerU sometimes garbles complex tables. Reconstruct from your source before submission.
- **No corpus caching yet.** Phase 1 re-runs each session. If you re-run for the same journal, point to the existing `journal_writing_rules.md` and skip Phase 1 manually.
- **English manuscripts only.** The skill and base rules assume English-language academic writing.
- **Disciplines not covered.** Medicine, law, social sciences, biology — no built-in base rules. Use your own or skip.

---

## Contributing

Pull requests welcome, especially:
- New `base_rules/` files for uncovered disciplines
- Improvements to existing base rules
- Bug reports from real revision runs

One file per discipline. Follow the structure in any existing `base_rules/` file.

---

## Example corpus structure

```
my_journal_pdfs/
├── paper_001.pdf
├── paper_002.pdf
├── ...
└── paper_008.pdf        ← 5–8 papers is enough for strong signals
```

No special naming required. The skill reads all PDFs in the folder.

---

## License

MIT
