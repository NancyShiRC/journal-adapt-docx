# Example: JEEM Dynamic Writing Skill MVP (Anonymized)

This example shows an anonymized MVP run of the revised journal-adapt workflow.

Target journal: **Journal of Environmental Economics and Management (JEEM)**  
Manuscript: anonymized working paper on carbon pricing and distributional policy  
Status: public example, sanitized

No unpublished manuscript text, author names, private file paths, exact numerical findings, or manuscript-specific model details are included.

---

## What This Example Demonstrates

This example tests the new dynamic framework:

1. **Primary corpus:** JEEM papers are used to learn target-journal writing patterns.
2. **Secondary corpus:** non-JEEM but field-relevant papers are optional support, not target-journal evidence.
3. **Static base skill:** the bundled economics base rules provide fallback writing rules.
4. **Conversion gate:** only fully readable converted files enter Phase 1.
5. **Dynamic skill:** Phase 1 generates a reviewable `dynamic_writing_skill.md`.
6. **Section revision:** Phase 2 revises a manuscript section using only the dynamic skill and the manuscript section.

---

## Files

| File | Purpose |
|------|---------|
| `corpus_meta.yaml` | Public corpus-role metadata for the anonymized MVP. |
| `conversion_report.md` | Shows the conversion gate and retry rule. |
| `style_profile.md` | Aggregated JEEM and secondary-corpus writing patterns. |
| `dynamic_writing_skill.md` | The generated anonymized dynamic writing skill. |
| `section_diagnosis_sample.md` | Sanitized sample diagnosis for one manuscript section. |
| `section_revision_sample.md` | Sanitized before/after example using placeholder text. |
| `section_revision_log_sample.md` | Sanitized revision log showing rule application. |

Raw PDFs, converted full texts, and the manuscript are not included.

---

## Corpus Roles

The MVP used:

- JEEM papers as the **primary target-journal corpus**;
- field-relevant papers from environmental economics, climate economics, and policy journals as the **optional secondary corpus**;
- bundled economics rules as the **static base skill**;
- no user/lab exemplars.

Secondary-corpus patterns are not allowed to override reviewed JEEM patterns unless the user explicitly chooses that behavior.

---

## Privacy Boundary

This example is intentionally anonymized. It keeps:

- workflow structure;
- corpus-role logic;
- target-journal writing patterns;
- dynamic-skill format;
- sanitized revision examples.

It removes:

- working paper title;
- author names and affiliations;
- private file paths;
- exact calibrated numbers;
- manuscript-specific model names and variables;
- full paragraph rewrites from the unpublished manuscript.

Use this folder as a public demonstration of the revised workflow, not as evidence about the private working paper.
