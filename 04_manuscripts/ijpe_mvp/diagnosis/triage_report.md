# Section Triage Report

date: 2026-05-01
manuscript: ijpe_mvp
skill_used: SKILL_IJPE_20260501.md
phase: Phase 2 only; corpus, paper style cards, and journal style card not loaded

| Section | Paragraphs | Est. Match Score | Highest Severity | Priority | Recommended Mode |
|---------|------------|------------------|------------------|----------|------------------|
| Abstract | 1 | 4 | MED | HIGH | Mode A: 3-round |
| Introduction | 8 | 5 | LOW | HIGH | Mode A: 3-round |
| Literature Review | 17 | 4 | MED | MED | Mode B: merged |
| Methods/Model | 33+ | 4 | MED | MED | Mode B: merged |
| Simulation/Results | 15+ plus tables/figures | 3 | MED | LOW-MED | Mode C fast scan plus targeted prose notes |
| Discussion | 10 | 4 | MED | MED | Mode B: merged |
| Conclusion | 3 | 4 | LOW | LOW | Mode C fast scan |

## Top Problems by Section

**Abstract.** The abstract is already close to IJPE style because it identifies the operational problem, ownership decision, Stackelberg model, ownership structures, contract mechanism, and calibration boundary. The main fix is compression: the current version reads as a dense summary of every mechanism. It should foreground the decision problem and keep simulation/calibration as scenario discipline rather than as a long data list.

**Introduction.** The revised introduction already matches the active SKILL: operational context, ownership gap, explicit RQs, conceptual model preview, concrete contributions, and roadmap. Only low-severity polishing is needed before final manuscript integration, mainly consistency of terms such as `Battery-as-a-Service`, `service level`, and `lifecycle responsibility`.

**Literature Review.** The section has the right thematic architecture, but some paragraphs summarize streams before converting them into the ownership/contract/lifecycle gap. Several transition sentences can be made more IJPE-like by specifying the missing decision object rather than saying a topic is underexplored. The table extracted from PDF conversion is visibly corrupted and should be rebuilt from source before submission.

**Methods/Model.** The model follows the expected actor-to-notation sequence and keeps ownership structures comparable. The main issue is explanatory density around assumptions, generic downstream problem, and propositions. The prose should do more work to tell readers what each formal block is for, while equations, notation, proposition statements, and proof logic remain unchanged.

**Simulation/Results.** The simulation section correctly distinguishes data-disciplined calibration from causal estimation. The highest practical issue is not journal style but conversion/table integrity: Tables 3-5 and appendix tables need manual reconstruction from the source manuscript. Prose should keep emphasizing comparative statics, not empirical identification.

**Discussion.** The discussion is substantively strong but long. It can be tightened by grouping implications around three mechanisms: lifecycle capability, service-investment incentives, and platform coordination. Policy implications should remain bounded to traceability, health-state records, interoperability, recovery responsibility, and residual-value allocation.

**Conclusion.** The conclusion already synthesizes the model and implications. It only needs a short anti-template pass: reduce repeated setup, keep future research specific, and avoid reopening the literature review.

## Approved Run Order for This Session

1. Abstract — Mode A output written as a polished revised section.
2. Introduction — Mode A uses existing `introduction_v2.md` as the accepted baseline.
3. Literature Review — Mode B merged diagnosis and revision.
4. Methods/Model — Mode B targeted prose revision notes and replacement paragraphs.
5. Simulation/Results — Mode C fast scan with targeted prose replacement for calibration framing.
6. Discussion — Mode B merged revision.
7. Conclusion — Mode C fast scan with a concise revised version.
