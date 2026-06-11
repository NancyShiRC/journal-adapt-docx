# Installation and PDF Conversion

This guide separates two things that are often confused:

1. installing the journal-adapt skill,
2. converting PDFs into Markdown.

You only need a PDF converter when your corpus or manuscript is in PDF form. If you already have Markdown or plain text, you can skip MinerU entirely.

---

## Install the Skill

### Claude Code

From the repository root:

```bash
mkdir -p ~/.claude/skills/journal-adapt
cp -R skill/* ~/.claude/skills/journal-adapt/
```

Then invoke:

```text
/journal-adapt
```

or ask:

```text
Help me build a dynamic writing skill for this manuscript.
```

### Codex

Codex custom-skill installation depends on your local setup.

Recommended options:

- keep this repository open and ask Codex to follow `skill/SKILL.md`;
- copy or symlink `skill/` into your local Codex skills directory if your installation supports it;
- paste the path to `skill/SKILL.md` when asking Codex to run the workflow.

Local Codex example:

```bash
mkdir -p ~/.codex/skills/journal-adapt-writing-skill
cp -R skill/* ~/.codex/skills/journal-adapt-writing-skill/
```

---

## Recommended Input Path: Markdown

The most reliable workflow is to provide Markdown or plain text files:

```text
project/
├── corpus/
│   ├── target_journal_001.md
│   ├── target_journal_002.md
│   └── field_top_paper_001.md
└── manuscript.md
```

This avoids PDF conversion problems and does not require MinerU.

---

## PDF Input Path

If your inputs are PDFs, convert them to Markdown before style extraction.

MinerU is supported:

```bash
pip install mineru
mineru --version
```

Then convert one file at a time:

```bash
python3 -m mineru.cli.pdf_to_md "path/to/paper.pdf" --output-dir "converted/paper_001/"
```

Do not rely on large batch conversion for a whole corpus. Converting one PDF at a time makes failures easier to isolate and avoids incomplete batch output on some machines.

---

## If MinerU Fails

MinerU is useful, but it is not part of the writing logic. If installation or conversion fails, use one of these paths:

1. Export the PDF to Markdown, text, or Word using another tool.
2. Use the publisher's HTML page and save the article text as Markdown, if available and legally accessible.
3. Ask the user for a clean Markdown/text version of the paper.
4. Replace the paper with another corpus paper if conversion still fails.

The workflow can continue as long as every corpus paper used in Phase 1 has fully readable text. It does not require MinerU specifically.

---

## Quality Check After Conversion

Before extraction, quickly inspect the converted text:

- section order is readable;
- equations are preserved as LaTeX or clear text;
- citations and references are not collapsed into unrelated paragraphs;
- tables are not silently garbled;
- the manuscript's technical terms and variables are intact.

If conversion damages equations, tables, or notation, fix the source text before revision. journal-adapt preserves what it sees; it cannot recover technical content lost during conversion.

After checking, use only fully readable files for style extraction. If a file is partial or failed, retry conversion, use another converter, ask the user for Markdown/text, or replace the paper. Partial and failed conversions should not enter regular dynamic-skill generation.

---

## Troubleshooting Notes

Common symptoms:

| Symptom | Likely cause | Workaround |
|---------|--------------|------------|
| `mineru: command not found` | executable not on PATH | Use Markdown input or call MinerU through its full environment path. |
| Python module not found | installed in a different Python environment | Run `python3 -m pip show mineru` and use the matching Python executable. |
| Batch conversion crashes | too many PDFs processed at once | Convert one PDF at a time. |
| Output Markdown is unreadable | PDF layout, OCR, or table extraction issue | Manually clean the converted Markdown or use another converter. |
| Skill refuses to start without MinerU | old skill version | Update `skill/SKILL.md`; current versions only require MinerU for PDF inputs. |

When in doubt, use Markdown input. The dynamic writing skill logic starts after conversion.

---

## Word DOCX Input With EndNote / CWYW Fields

Do not convert a DOCX manuscript to Markdown when it contains EndNote, Cite While You Write, Zotero, Mendeley, Word field codes, generated bibliography, automatic numbering, captions, cross-references, or other Word automation that must be preserved.

For these manuscripts, use the tracked-changes path:

1. Keep the original DOCX untouched.
2. Create a duplicate named like `[original_stem]_journal_adapt_tracked.docx`.
3. Open the duplicate in WPS Writer.
4. Enable revision/tracked-changes mode before editing.
5. Revise ordinary prose in place, section by section.
6. Avoid deleting or recreating citation fields, bibliography fields, cross-references, captions, equation objects, comments, and footnotes.
7. Save the duplicate and review the tracked changes manually in WPS or Word.

This preserves field codes and lets the author decide which edits to accept.
