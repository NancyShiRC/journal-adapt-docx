# MVP Test Log — IJPE Introduction

**Date:** 2026-05-01  
**Target journal:** International Journal of Production Economics  
**Manuscript slug:** ijpe_mvp  
**Method type:** model+simulation+calibration  
**Target section:** introduction

## PDF-to-Markdown Conversion

- Tool used: local `mineru-pdf-md` wrapper around MinerU CLI.
- Manuscript conversion succeeded.
  - Input: `04_manuscripts/ijpe_mvp/input/manuscript.pdf`
  - Output: `04_manuscripts/ijpe_mvp/converted/agent_readable.md`
  - Exit code: 0
- IJPE corpus batch conversion partially succeeded.
  - Input: `01_corpus/International_Journal_of_Production_Economics/raw/`
  - Output: `01_corpus/International_Journal_of_Production_Economics/converted/agent_readable.md`
  - Exit code: 1
  - Completed: 2 PDFs converted to Markdown.
  - Failed/interrupted: remaining batches returned service unavailable after long processing.

## MinerU Batch Failure — Root Cause (diagnosed 2026-05-01)

**Root cause:** Folder-mode conversion (`pdf_to_agent_md.py` given a directory) triggers MinerU's internal HTTP server, which splits PDFs into batches and processes them in parallel. The server crashed during Batch 2 at MFR Predict 94%, causing Batches 2 and 3 to fail with `503 Service Unavailable`.

```
Batch 1: completed — 2 PDFs converted (ijpe_005, ijpe_007)
Batch 2: failed — 503 mid-processing (ijpe_008, ijpe_001, ijpe_003)
Batch 3: failed — 503 on submit (ijpe_006, ijpe_002, ijpe_004)
```

**Fix:** Convert each PDF individually. Per-file mode starts one MinerU process per PDF without a persistent server, so it does not hit the batch crash. See MODULES.md Module 0 for the exact command.

**Remaining work to complete corpus:**
```bash
# 6 PDFs not yet converted:
python3 ~/.codex/skills/mineru-pdf-md/scripts/pdf_to_agent_md.py \
  "01_corpus/International_Journal_of_Production_Economics/raw/1-s2.0-S092552731630158X-mainext.pdf" \
  --output-dir "01_corpus/International_Journal_of_Production_Economics/converted/ijpe_001"

python3 ~/.codex/skills/mineru-pdf-md/scripts/pdf_to_agent_md.py \
  "01_corpus/International_Journal_of_Production_Economics/raw/1-s2.0-S0925527316302912-main.pdf" \
  --output-dir "01_corpus/International_Journal_of_Production_Economics/converted/ijpe_002"

python3 ~/.codex/skills/mineru-pdf-md/scripts/pdf_to_agent_md.py \
  "01_corpus/International_Journal_of_Production_Economics/raw/1-s2.0-S0925527319300295-main.pdf" \
  --output-dir "01_corpus/International_Journal_of_Production_Economics/converted/ijpe_003"

python3 ~/.codex/skills/mineru-pdf-md/scripts/pdf_to_agent_md.py \
  "01_corpus/International_Journal_of_Production_Economics/raw/1-s2.0-S0925527321000116-main.pdf" \
  --output-dir "01_corpus/International_Journal_of_Production_Economics/converted/ijpe_004"

python3 ~/.codex/skills/mineru-pdf-md/scripts/pdf_to_agent_md.py \
  "01_corpus/International_Journal_of_Production_Economics/raw/1-s2.0-S0925527325000362-main.pdf" \
  --output-dir "01_corpus/International_Journal_of_Production_Economics/converted/ijpe_006"

python3 ~/.codex/skills/mineru-pdf-md/scripts/pdf_to_agent_md.py \
  "01_corpus/International_Journal_of_Production_Economics/raw/1-s2.0-S0925527325003639-main.pdf" \
  --output-dir "01_corpus/International_Journal_of_Production_Economics/converted/ijpe_008"
```

After conversion: generate Paper Style Cards for all 8 papers, regenerate Journal Style Card with STRONG signals, update SKILL.md, re-run diagnosis and revision.

## Per-PDF Conversion Rerun — Completed 2026-05-01

The 6 PDFs that failed in folder-mode conversion were rerun one by one with the commands above. All 6 completed successfully.

| Paper ID | Output |
| --- | --- |
| `ijpe_001` | `01_corpus/International_Journal_of_Production_Economics/converted/ijpe_001/agent_readable.md` |
| `ijpe_002` | `01_corpus/International_Journal_of_Production_Economics/converted/ijpe_002/agent_readable.md` |
| `ijpe_003` | `01_corpus/International_Journal_of_Production_Economics/converted/ijpe_003/agent_readable.md` |
| `ijpe_004` | `01_corpus/International_Journal_of_Production_Economics/converted/ijpe_004/agent_readable.md` |
| `ijpe_006` | `01_corpus/International_Journal_of_Production_Economics/converted/ijpe_006/agent_readable.md` |
| `ijpe_008` | `01_corpus/International_Journal_of_Production_Economics/converted/ijpe_008/agent_readable.md` |

## MVP Decision

Initial weak-signal MVP was superseded after all 8 corpus PDFs were converted. The current MVP now uses:

- 8 converted IJPE papers for full-corpus journal-style signals.
- Converted manuscript Markdown for introduction extraction.
- STRONG journal-style labels only where supported by at least 3 papers or at least 60% of the corpus.
