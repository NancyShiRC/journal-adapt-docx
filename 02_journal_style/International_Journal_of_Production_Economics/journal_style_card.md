# Journal Style Card — International Journal of Production Economics

```yaml
journal: "International Journal of Production Economics"
papers_analyzed: 8
paper_ids: [ijpe_001, ijpe_002, ijpe_003, ijpe_004, ijpe_005, ijpe_006, ijpe_007, ijpe_008]
topic_scope: ["battery supply chains", "closed-loop supply chains", "battery lifecycle", "contract design", "EV battery recycling", "resilience"]
method_scope: "model+simulation+calibration"
generated_date: "2026-05-01"
reviewed_by: "pending"
signal_definitions:
  STRONG: ">=3 papers agree or >=60% of corpus"
  WEAK: "1-2 papers only"
  ABSENT: "pattern not observed in converted corpus"
  CONTESTED: "papers contradict each other on this dimension"
```

## 1. Editorial Identity

**What problems does this journal value?**  
IJPE values production, operations, and supply-chain problems where a managerial or policy decision changes system performance. In this corpus, the valued problems include who should collect or own recoverable products, how supply-chain members coordinate, how subsidies or contracts alter incentives, how lifecycle responsibility affects economic and sustainability outcomes, and how closed-loop or circular systems should be designed.

**What methods signal quality here?**  
Game-theoretic modeling, Stackelberg structures, centralized/decentralized comparisons, stochastic programming, systematic reviews, numerical experiments, and sensitivity analysis all appear. For model-based papers, the introduction should motivate why the model structure fits the managerial decision before moving into equations.

**Disciplinary stance:**  
Production economics and operations management dominate, with sustainability, policy, and circular-economy language used when tied to supply-chain decisions.

**Implied reader:**  
Academic specialists in operations/supply-chain management who also value managerial and policy implications.

## 2. Introduction Conventions

| Pattern | Signal | Supporting Papers |
|---------|--------|------------------|
| Opens with an industry, sustainability, recovery, or policy problem before narrowing to the model object | STRONG | ijpe_001, ijpe_002, ijpe_003, ijpe_004, ijpe_005, ijpe_006, ijpe_007, ijpe_008 |
| Moves from practical consequence to supply-chain design or coordination problem | STRONG | ijpe_001, ijpe_002, ijpe_004, ijpe_005, ijpe_006, ijpe_007, ijpe_008 |
| Uses early quantitative or institutional context when relevant | STRONG | ijpe_001, ijpe_003, ijpe_004, ijpe_005, ijpe_006, ijpe_007, ijpe_008 |
| Gap is stated after context and targeted literature positioning | STRONG | ijpe_001, ijpe_003, ijpe_004, ijpe_005, ijpe_006, ijpe_007, ijpe_008 |
| Research questions appear explicitly | STRONG | ijpe_001, ijpe_002, ijpe_003, ijpe_004, ijpe_005, ijpe_006, ijpe_007, ijpe_008 |
| Contributions are listed or sequenced explicitly | STRONG | ijpe_001, ijpe_005, ijpe_008 |
| Conventional roadmap closes the introduction | STRONG | ijpe_001, ijpe_002, ijpe_003, ijpe_004, ijpe_005, ijpe_006, ijpe_007 |

**Observed intro structure (most common):**  
Operational/sustainability context -> supply-chain consequence -> specific unresolved coordination/design/lifecycle gap -> research questions -> model or review method preview -> concrete contributions -> roadmap.

**What intros in this journal do NOT do:**
- They do not open with a detached literature survey.
- They do not present a model before motivating the managerial decision.
- They do not use generic contribution claims without specifying the operational mechanism.

## 3. Contribution Expression

| Pattern | Signal | Supporting Papers |
|---------|--------|------------------|
| Contribution tied to model structure, decision variable, contract, policy, framework, or method | STRONG | ijpe_001, ijpe_002, ijpe_003, ijpe_004, ijpe_005, ijpe_008 |
| Explicit RQs before contributions or model preview | STRONG | ijpe_001, ijpe_002, ijpe_003, ijpe_004, ijpe_005, ijpe_006, ijpe_007, ijpe_008 |
| Numbered or bullet contribution lists are acceptable when concrete | STRONG | ijpe_001, ijpe_005, ijpe_008 |
| Broad "first to study" language is not central | ABSENT | all converted papers |

**Preferred contribution format:**  
State the operational object, then give concrete advances. A model-based paper should map each contribution to a decision setting, model feature, contract mechanism, data/simulation feature, or managerial implication.

**Contribution claim strength:**  
Direct but bounded. The claim should not exceed what the model, simulation, or review can support.

## 4. Literature Review

| Pattern | Signal | Supporting Papers |
|---------|--------|------------------|
| Literature positioning is integrated into the introduction before formal modeling | STRONG | ijpe_001, ijpe_003, ijpe_004, ijpe_005, ijpe_008 |
| Separate literature review section is acceptable after a targeted intro gap | STRONG | ijpe_002, ijpe_004, ijpe_005 |
| Organization by theme/decision stream rather than chronology | STRONG | ijpe_002, ijpe_004, ijpe_005, ijpe_006, ijpe_007 |

**How literature is positioned:**  
Prior work is used to justify the missing decision dimension, such as ownership, recovery channel, subsidy allocation, lifecycle responsibility, resilience, or circular-supply-chain scope.

## 5. Method / Model Norms

| Pattern | Signal | Supporting Papers |
|---------|--------|------------------|
| Practical system and decision structure appear before notation | STRONG | ijpe_001, ijpe_002, ijpe_003, ijpe_004, ijpe_005, ijpe_008 |
| Stackelberg, centralized/decentralized, and contract comparisons are normal | STRONG | ijpe_001, ijpe_002, ijpe_003, ijpe_005 |
| Numerical experiments, sensitivity analysis, or case validation are expected for model-based papers | STRONG | ijpe_002, ijpe_003, ijpe_004, ijpe_005, ijpe_008 |
| Data-driven or real-case calibration strengthens model papers | WEAK | ijpe_005, ijpe_008 |

**Notation density standard:**  
High notation is acceptable after the problem is motivated. The introduction should remain conceptual and managerial.

**Formal exposition style:**  
System boundary -> actors and decisions -> assumptions -> model cases -> equilibrium/comparison -> numerical analysis.

## 6. Results and Discussion Norms

| Pattern | Signal | Supporting Papers |
|---------|--------|------------------|
| Results narrative compares structures/policies/models | STRONG | ijpe_001, ijpe_002, ijpe_003, ijpe_004, ijpe_005, ijpe_008 |
| Mechanism explanation matters, not only sign or optimal value | STRONG | ijpe_001, ijpe_003, ijpe_004, ijpe_005, ijpe_008 |
| Managerial or policy implications are expected | STRONG | ijpe_003, ijpe_004, ijpe_005, ijpe_008 |

**Discussion function in this journal:**  
Discussion should explain why one structure, policy, or contract performs better and under what parameter or scenario conditions.

**Policy implications scope:**  
Policy statements are acceptable when they follow directly from the model or review.

## 7. Language Style Profile

| Dimension | This Journal's Norm | Signal |
|-----------|--------------------|--------|
| Voice | mixed; active acceptable for RQs and contributions | STRONG |
| Sentence length | medium to long, but paragraph roles are explicit | STRONG |
| Register | technical production/supply-chain with sustainability or policy when relevant | STRONG |
| Hedging level | moderate; direct claims are scoped to model/review | STRONG |
| Mathematical density | high after the introduction, low in intro | STRONG |
| Transition style | explicit research questions, contribution sequencing, roadmap | STRONG |

## 8. Conflict Table: Journal Norms vs General Econ Writing Rules

| Dimension | General Econ Rule | This Journal's Norm | Winner | Notes |
|-----------|------------------|--------------------|--------|-------|
| Contribution format | 2-3 sharp claims often preferred | Numbered or bullet contribution lists acceptable when concrete | Journal | STRONG |
| Intro length | Keep compact | Developed introductions acceptable if each paragraph advances context, gap, method, or contribution | Journal | STRONG |
| Roadmap | Optional | Conventional roadmap is common | Journal | STRONG |
| Policy language | Academic register | Policy and managerial implications acceptable when model-grounded | Journal | STRONG |
| Literature placement | Avoid opening with literature | IJPE also avoids literature-first openings; targeted literature comes after problem framing | Tie | STRONG |

## 9. Red Flags

- Opening with a pure literature review rather than the production or supply-chain problem.
- Listing generic contributions that are not tied to ownership, contract, subsidy, lifecycle, recovery, resilience, or model structure.
- Presenting equations or notation before explaining actors, decisions, and managerial stakes.
- Making policy claims not supported by the model or simulation.
- Treating simulation/calibration details as decoration rather than as discipline for model scenarios.

## 10. Human Reviewer Notes

**Patterns I agree with (strong signals confirmed):**
-

**Patterns I disagree with (AI overread):**
-

**Patterns AI missed:**
-

**My overall judgment of this journal's writing culture:**
[pending]
