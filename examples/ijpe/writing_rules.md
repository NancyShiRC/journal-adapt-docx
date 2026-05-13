# Temporary SKILL.md — International Journal of Production Economics

```yaml
skill_type: journal-adaptive-writing
target_journal: "International Journal of Production Economics"
target_sections: ["abstract", "introduction", "literature_review", "methods_model", "results", "discussion", "conclusion"]
paper_type: "model+simulation+calibration"
base_skill: "econ_writing_base.md"
generated_from: "02_journal_style/International_Journal_of_Production_Economics/journal_style_card.md"
created_date: "2026-05-01"
priority_version: 1
status: "active"
evidence_level: "8-paper corpus"
```

## PART 1 — PRIORITY RULES

### Priority 1 — HARD PRESERVE

Preserve all facts, citations, model objects, actor names, research questions, numerical claims, section references, and terminology unless the user explicitly approves a change. Do not add new empirical facts, citations, model results, or policy claims.

### Priority 2 — STRONG FOLLOW

Apply IJPE strong-signal patterns:

- Start from an industry, sustainability, recovery, or operational problem.
- Narrow quickly to the supply-chain design or coordination decision.
- State the unresolved ownership/contract/lifecycle gap after context and targeted literature positioning.
- Use explicit research questions.
- Give concrete contributions tied to model structure, decision variables, contracts, lifecycle responsibility, data/calibration, or managerial implications.
- Keep formal notation out of the introduction; preview the model conceptually.
- End with a conventional roadmap.

### Priority 3 — DEFAULT APPLY

Apply the base economic writing rules when IJPE gives no specific rule: one idea per paragraph, clear topic sentence, evidence after claim, no unsupported causal language, and no generic contribution claims.

### Priority 4 — ALWAYS REMOVE

Remove generic AI-taste phrases, hollow transitions, and broad contribution statements that do not name the operational mechanism.

## LOADING INSTRUCTION FOR REVISION SESSIONS

When running Phase 2 revision, load this SKILL.md only. Do not load corpus papers, Paper Style Cards, or the Journal Style Card. For each section call, use Part 1, the relevant Part 2 block, Parts 3-5, and the current manuscript section only.

## PART 2 — SECTION-SPECIFIC GUIDANCE

### Part 2A — Abstract

**Revision mode:** HIGH — apply all rules fully.

**Journal norm:** Move from operational context to specific supply-chain decision, then to model approach and tightly scoped contribution. Keep the abstract technical and concrete; do not use broad sustainability or platform-economy language unless it is already supported by the manuscript.

**Structure:** context/problem -> unresolved ownership/coordination issue -> model and comparison objects -> simulation/calibration role -> main implication stated without overclaiming.

**Tense:** Present tense for problem, model purpose, and implications; past tense only for actions already performed in the study.

**Contribution placement:** State the paper's contribution through the decision object and model comparison, not through generic "contributes to the literature" phrasing.

**Guidance:**
- Name the focal service model, the key ownership/contract decision, and lifecycle responsibility early.
- Preview the game-theoretic model and ownership/contract structures without notation.
- Mention simulation/calibration as disciplining scenarios, not as external causal proof.
- Preserve all numerical claims, datasets, and citations if present.

**Do not:**
- Do not add results or quantitative claims not already in the abstract.
- Do not use "This paper explores" or similar AI-taste openers.
- Do not turn the abstract into a mini-introduction with lengthy literature positioning.

### Part 2B — Introduction

**Journal norm:** Operational/sustainability context -> supply-chain consequence -> specific unresolved ownership/coordination/lifecycle gap -> research questions -> model preview -> concrete contributions -> roadmap.

**Opening move:** Begin with the focal operational setting where downtime, asset utilization, and service network design matter. Move to the focal service model quickly.

**Problem framing:** State how the focal service model transforms the asset from a sold component into a circulating lifecycle asset. Make ownership a supply-chain design decision because it assigns capital cost, quality control, residual value, service investment, and recovery responsibility.

**Gap statement:** Position the gap as a combined ownership-contract-lifecycle gap. Prior work on operations, adoption, and routing is not enough because it often leaves asset ownership and coordination terms fixed.

**Research questions:** Keep your research questions explicit.

**Method preview:** Preview the game-theoretic model and the ownership/contract structures before discussing simulation and calibration.

**Contribution format:** Use an explicit contribution paragraph or list. Each contribution should map to one concrete element:

- the model's primary decision object (ownership and contract design) rather than lower-level operational optimization;
- lifecycle responsibility and residual value in the game-theoretic model;
- analytical conditions for ownership/contract preference;
- data-disciplined simulation and transparent scenario parameters.

**Roadmap:** Retain a standard roadmap paragraph.

### Part 2C — Literature Review

**Revision mode:** MED by default.

**Journal norm:** Organize by decision stream and mechanism rather than chronology. Each subsection should end by clarifying what is still unresolved for ownership, coordination, lifecycle responsibility, or calibration in the focal service setting.

**Structure:** thematic stream -> what that stream explains -> what it leaves fixed or external -> how this paper uses or extends the stream.

**Positioning move:** Contrast prior work by decision object, actor structure, lifecycle scope, and coordination mechanism. Avoid claiming a literature is simply "limited"; specify the missing decision or channel.

**Citation density:** Preserve existing citations. Do not add new citations. If a paragraph has citations, keep them attached to the claim they support.

**Common failure:** Literature paragraphs that summarize topics without converting them into a supply-chain design gap.

**Do not:**
- Do not create new literature claims or add new references.
- Do not overstate novelty as "first" unless the original already says so.
- Do not collapse distinct streams if their section headings are useful.

### Part 2D — Methods / Model

**Revision mode:** MED by default.

**Journal norm:** Present actors, decisions, timing, assumptions, and ownership structures before heavy notation. Formal derivations can be dense, but the economic intuition for each block should be visible.

**Entry point:** Start from system boundary and actor roles; then move into assumptions, demand, costs, profit functions, and equilibrium.

**System description:** Make ownership structures comparable by using consistent language for the model actors, ownership/contract terms, service levels, and lifecycle responsibility.

**Exposition style:** Use proposition-then-intuition or result-then-mechanism where possible. Keep equations and notation unchanged.

**Notation density:** Preserve all notation. Improve prose around notation only when it helps readers understand what a variable represents.

**Assumption justification:** Keep justifications short and tied to the operational setting. Do not add empirical support that is not already in the manuscript.

**Verification:** Simulation/calibration should be framed as scenario discipline and robustness support, not as proof beyond model assumptions.

**Do not:**
- Do not alter equations, variables, parameter definitions, or optimization problems.
- Do not change the model sequence or ownership cases.
- Do not add new assumptions.

### Part 2E — Results / Simulation

**Revision mode:** LOW to MED depending on triage severity.

**Journal norm:** Results narration should compare structures, identify mechanisms, and connect parameter changes to managerial or policy implications without repeating the model setup.

**Narration style:** result/comparison -> mechanism -> implication for ownership, contract, lifecycle responsibility, or service design.

**Comparison structure:** Keep comparisons aligned across the ownership and contract structures in the model where applicable.

**Mechanism emphasis:** Required. Explain why a pattern occurs through price distortion, service investment, recovery responsibility, residual value, or coordination terms.

**Robustness:** Present robustness as checking whether ownership and contract insights survive parameter variation. Do not overstate calibration.

**Quantitative claims:** Preserve every numerical result and figure/table reference exactly.

**Do not:**
- Do not introduce new numerical results.
- Do not convert scenario analysis into empirical causal evidence.
- Do not restate equations unless needed to interpret a result.

### Part 2F — Discussion and Policy Implications

**Revision mode:** MED by default.

**Journal norm:** Discussion should translate model mechanisms into bounded managerial and policy implications. Claims may reach practice, but only through the model's ownership, contract, service-level, and lifecycle channels.

**Function:** Explain what the results imply for platform governance, actor incentives, service coordination, and recovery responsibility beyond the formal model.

**Scope of claims:** Generalize cautiously. Use "suggests", "indicates", or "is consistent with" when moving from model/simulation to practice.

**Policy language register:** Technical and production-economics oriented. Recommendations should identify the responsible actor or contract lever.

**Limitation acknowledgment:** Brief but explicit. State limitations as boundaries of the model and data rather than apologetic weakness.

**Do not:**
- Do not rehash the results section.
- Do not make broad industrial-policy claims unsupported by the model.
- Do not add new empirical evidence or new cases.

### Part 2G — Conclusion

**Revision mode:** LOW by default.

**Journal norm:** Concise synthesis of the problem, model comparison, central insight, and bounded implication. The conclusion should not reopen the literature review.

**Function:** Remind readers what decision the model clarifies and why the focal ownership/contract/lifecycle decision matters in the study setting.

**Length:** Short to medium. Remove repeated setup if the conclusion restates the introduction.

**Future research:** Optional. If included, make it specific to data, behavior, contracts, lifecycle operations, or market heterogeneity.

**Do not:**
- Do not introduce new claims, citations, or mechanisms.
- Do not use template endings such as "future research should further explore".
- Do not overstate simulation/calibration as validation beyond available data.

## PART 3 — CONFLICT RESOLUTIONS

| Dimension | General Rule | This Journal | Resolution | Signal |
|-----------|--------------|--------------|------------|--------|
| Contribution format | Prefer a small number of sharp claims | Explicit lists acceptable when concrete | Use four concrete contributions if each maps to a model element | STRONG |
| Intro length | Keep compact | Developed intro acceptable | Keep current developed structure but tighten generic language | STRONG |
| Roadmap | Optional | Conventional roadmap common | Retain roadmap | STRONG |
| Policy language | Avoid broad claims | Policy/managerial language accepted when model-grounded | Keep lifecycle and recovery policy implications bounded | STRONG |
| Literature placement | Do not open with literature | Same journal norm | Begin with operational context, not literature | STRONG |

## PART 4 — SIGNAL-WEAK FLAGS

- SIGNAL-WEAK: Real-case or data-driven calibration strengthens model papers but is only directly supported by two corpus papers. Apply as a support feature, not a central journal requirement.

## PART 5 — LANGUAGE REGISTER CALIBRATION

- **Voice:** Use active voice for research questions and contributions; passive is acceptable for established processes.
- **Sentence length:** Medium-length sentences preferred; longer sentences are acceptable when they define a supply-chain mechanism.
- **Hedging:** Use direct claims when describing the paper's model; hedge only when interpreting empirical calibration or policy scope.
- **Mathematical prose:** Introduce actors and decisions conceptually before any notation.
- **Transitions:** Prefer explicit structural transitions such as "To answer these questions" and "The model compares."
- **Formality:** Technical, production-economics style; avoid marketing-like language.

## PART 6 — QUICK REFERENCE CHECKLIST

```
□ No new facts, citations, or model results added
□ Battery ownership framed as supply-chain design, not accounting
□ Research questions explicit
□ Model preview before contributions
□ Contributions concrete and model-specific
□ Lifecycle responsibility and recovery incentives retained
□ Simulation/calibration described as scenario discipline, not proof beyond scope
□ Roadmap retained
```

