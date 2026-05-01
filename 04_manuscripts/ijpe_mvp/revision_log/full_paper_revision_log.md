# Full-Paper Revision Log

date: 2026-05-01
manuscript: ijpe_mvp
skill_used: SKILL_IJPE_20260501.md
phase: Phase 2 only; corpus artifacts were not loaded

## Session Entry Check

- Active SKILL.md exists: yes.
- SKILL status: active.
- Coverage: Abstract, Introduction, Literature Review, Methods/Model, Results, Discussion, Conclusion.
- Action taken: proceeded directly to Module E0 and Module E.
- Corpus, Paper Style Cards, Journal Style Card: not read during revision.

## Section Decisions

| Section | Mode | Output |
|---------|------|--------|
| Abstract | Mode A | `revised/full_paper/abstract_v1.md` |
| Introduction | Mode A | `revised/introduction_v2.md` retained as current accepted baseline |
| Literature Review | Mode B | `revised/full_paper/literature_review_v1.md` |
| Methods/Model | Mode B | `revised/full_paper/methods_model_v1.md` |
| Simulation/Results | Mode C | `revised/full_paper/simulation_results_fast_scan.md` |
| Discussion | Mode B | `revised/full_paper/discussion_v1.md` |
| Conclusion | Mode C with light rewrite | `revised/full_paper/conclusion_v1.md` |

## Reusable Rule Candidates

1. **For IJPE model papers, every literature-review stream should end by naming the unresolved decision object, not by saying the area is underexplored.**
   - Target skill: this-journal-only
   - Condition: literature review for model+simulation+calibration papers

2. **For BaaS or product-service models, distinguish asset ownership, operational control, and lifecycle responsibility before introducing notation.**
   - Target skill: journal-adaptive-general
   - Condition: methods/model sections with ownership or contract comparison

3. **For data-disciplined simulations, state the boundary between observed proxies and private scenario parameters before reporting results.**
   - Target skill: journal-adaptive-general
   - Condition: simulation/calibration sections without transaction-level data

4. **For discussion sections, organize managerial and policy implications by model mechanism rather than by actor list when the original section is long.**
   - Target skill: econ-base
   - Condition: discussion sections with repeated results and implications

## Integration Notes

- Equations, notation, proposition statements, citations, numerical results, and figure/table references were not changed.
- The converted manuscript contains table corruption from PDF-to-Markdown extraction. Tables 1, 3, 4, 5, A.7, and A.8 should be reconstructed from the source manuscript or original tables before submission.
- The new full-section outputs are Markdown revision drafts. They should be transferred into the author's manuscript source format after human approval.
