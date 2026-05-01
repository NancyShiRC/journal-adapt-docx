# Revision Log — Introduction

```yaml
manuscript_slug: ijpe_mvp
section: introduction
target_journal: "International Journal of Production Economics"
skill_used: "SKILL_IJPE_20260501.md"
revision_date: "2026-05-01"
total_paragraphs_revised: 4
total_paragraphs_unchanged: 4
```

## Entry 1

```yaml
entry_id: introduction-para-2
paragraph_number: 2
severity: MED
problem_types: [STYLE, LOGIC, JOURNAL-MISMATCH]
human_decision: pending
```

### Original Text

BaaS creates a new supply-chain boundary. The battery is no longer a component embedded in the vehicle at sale; it becomes a shared, depreciating, safety-critical, and recoverable asset. This asset can be owned by the vehicle manufacturer, the swapping operator, a platform, or an alliance of these actors. Ownership determines who bears battery capital cost, controls battery quality, captures residual value, takes responsibility for end-of-life recovery, and invests in swapping service level. Battery ownership is therefore an operational design decision, not an accounting detail. It allocates lifecycle risk and shapes the strategic interaction among OEMs, operators, platforms, and riders.

### Diagnosis

**Problem type(s):** [STYLE] [LOGIC] [JOURNAL-MISMATCH]

**Issues identified:**
- Ownership is correctly framed, but IJPE strong signals favor explicit supply-chain design and coordination vocabulary.
- The lifecycle-risk point should be linked more directly to recovery responsibility and incentives.

**Journal match score:** 4/5

### Revised Text

BaaS turns the battery into a shared supply-chain asset rather than a component embedded in the vehicle at sale. The battery is depreciating, safety-critical, recoverable, and repeatedly circulated through a service network. It can be owned by the vehicle manufacturer, the swapping operator, a platform, or an alliance of these actors. This ownership choice determines who bears battery capital cost, controls battery quality, captures residual value, takes responsibility for end-of-life recovery, and invests in swapping service level. Battery ownership is therefore a production and supply-chain design decision because it allocates lifecycle risk, coordination incentives, and recovery responsibility among OEMs, operators, platforms, and riders.

### Rationale

**Rules applied:**
- Frame ownership as supply-chain design — Source: journal-card (STRONG)
- Use production-economics register — Source: journal-card (STRONG)

**Conflict resolved?** no

**Signal-weak application?** no

**What was preserved verbatim:**
- Actor names: OEMs, operators, platforms, riders.
- Core claims about capital cost, quality control, residual value, recovery, and service level.

### Reusability Assessment

**Worth generalizing?** YES

- **Rule candidate:** "When adapting a model-based IJPE introduction, name the operational decision and the coordination incentives it reallocates before presenting the formal model."
- **Condition:** Model-based production/supply-chain papers.
- **Target skill:** journal-adaptive-general
- **Evidence strength:** consistent with 8-paper corpus

## Entry 2

```yaml
entry_id: introduction-para-3
paragraph_number: 3
severity: MED
problem_types: [LOGIC, JOURNAL-MISMATCH]
human_decision: pending
```

### Original Text

Recent battery swapping studies mainly examine station location, inventory planning, dispatching, grid interaction, vehicle routing, and user adoption. These models clarify important operating decisions, but they leave ownership and contract design for E2W BaaS less developed. The gap matters because two-wheeler markets combine fragmented demand, intense price competition, safety regulation, and heterogeneous usage. A delivery rider who swaps several times per day values the service differently from a private commuter who swaps occasionally. At the same time, the battery owner must invest in standardization, monitoring, maintenance, and recovery. When the battery owner and service operator are different firms, decentralized decisions can create double marginalization and service underinvestment.

### Diagnosis

**Problem type(s):** [LOGIC] [JOURNAL-MISMATCH]

**Issues identified:**
- Gap is accurate but should end by naming the combined ownership-contract-lifecycle problem.
- IJPE strong-signal introductions tie the gap to the decision structure being modeled.

**Journal match score:** 4/5

### Revised Text

Recent battery swapping studies mainly examine station location, inventory planning, dispatching, grid interaction, vehicle routing, and user adoption. These models clarify important operating decisions, but they leave ownership and contract design for E2W BaaS less developed. The gap matters because two-wheeler markets combine fragmented demand, intense price competition, safety regulation, and heterogeneous usage. A delivery rider who swaps several times per day values the service differently from a private commuter who swaps occasionally. At the same time, the battery owner must invest in standardization, monitoring, maintenance, and recovery. When the battery owner and service operator are different firms, decentralized decisions can create double marginalization and service underinvestment. The ownership question is therefore also a contract-design and lifecycle-responsibility question.

### Rationale

**Rules applied:**
- State the unresolved coordination/design/lifecycle gap — Source: journal-card (STRONG)
- Keep gap scoped to existing manuscript claims — Source: hard preserve

**Conflict resolved?** no

**Signal-weak application?** no

**What was preserved verbatim:**
- Existing literature categories and market-setting claims.
- No new citations, facts, or numerical claims added.

### Reusability Assessment

**Worth generalizing?** YES

- **Rule candidate:** "End the introduction gap paragraph by naming the exact decision bundle the model resolves."
- **Condition:** Model-based supply-chain papers with multiple linked decision dimensions.
- **Target skill:** journal-adaptive-general
- **Evidence strength:** consistent with 8-paper corpus

## Entry 3

```yaml
entry_id: introduction-para-5
paragraph_number: 5
severity: LOW
problem_types: [STYLE]
human_decision: pending
```

### Original Text

To answer these questions, we develop a Stackelberg game with an OEM, a swapping operator, and a platform coordinator. The OEM produces the vehicle body and may either retain batteries or transfer them to the operator. The operator manages swapping cabinets, charging, maintenance, and user-facing service. The platform coordinates demand access, settlement, service standards, and lifecycle records. Riders choose the BaaS service based on generalized ownership and usage costs, including the vehicle price, subscription fee, per-swap fee, and service level.

### Diagnosis

**Problem type(s):** [STYLE]

**Issues identified:**
- Paragraph already matches IJPE model-preview norms.
- No substantive rewrite needed.

**Journal match score:** 5/5

### Revised Text

To answer these questions, we develop a Stackelberg game with an OEM, a swapping operator, and a platform coordinator. The OEM produces the vehicle body and may either retain batteries or transfer them to the operator. The operator manages swapping cabinets, charging, maintenance, and user-facing service. The platform coordinates demand access, settlement, service standards, and lifecycle records. Riders choose the BaaS service based on generalized ownership and usage costs, including the vehicle price, subscription fee, per-swap fee, and service level.

### Rationale

**Rules applied:**
- Preview actors and decisions before notation — Source: journal-card (STRONG)

**Conflict resolved?** no

**Signal-weak application?** no

**What was preserved verbatim:**
- Entire paragraph preserved.

### Reusability Assessment

**Worth generalizing?** MAYBE

- **Rule candidate:** "When a paragraph already previews actors, decisions, and user choice clearly, preserve it rather than revising for style alone."
- **Condition:** Revision would not improve journal fit.
- **Target skill:** journal-adaptive-general
- **Evidence strength:** single case

## Entry 4

```yaml
entry_id: introduction-para-7
paragraph_number: 7
severity: MED
problem_types: [AI-TASTE, JOURNAL-MISMATCH]
human_decision: pending
```

### Original Text

The paper contributes in four ways. First, it shifts the battery swapping discussion from station-level optimization to supply-chain ownership and contract design. Second, it brings battery lifecycle responsibility into a BaaS Stackelberg model, linking service operations to recovery and residual value. Third, it derives analytical conditions under which OEM ownership, operator ownership, or platform coordination is preferred. Fourth, it uses observed swapping-station POIs, official spatial databases, and published charging, mobility, and battery studies to discipline the simulations, while treating private contractual terms as transparent scenario parameters.

### Diagnosis

**Problem type(s):** [AI-TASTE] [JOURNAL-MISMATCH]

**Issues identified:**
- The content is strong, but "contributes in four ways" is generic.
- IJPE strong-signal evidence supports explicit contribution sequencing when each item maps to a model feature.

**Journal match score:** 3/5

### Revised Text

This paper makes four contributions to the analysis of E2W BaaS supply chains. First, it shifts the battery swapping discussion from station-level optimization to ownership and contract design. Second, it brings battery lifecycle responsibility into a BaaS Stackelberg model, linking service operations to recovery and residual value. Third, it derives analytical conditions under which OEM ownership, operator ownership, or platform coordination is preferred. Fourth, it uses observed swapping-station POIs, official spatial databases, and published charging, mobility, and battery studies to discipline the simulations, while treating private contractual terms as transparent scenario parameters.

### Rationale

**Rules applied:**
- Use concrete, model-specific contribution statements — Source: journal-card (STRONG)
- Remove generic contribution wording — Source: econ-base and anti-AI-taste rule

**Conflict resolved?** yes
- IJPE permits explicit contribution sequencing; this overrides a general preference for shorter contribution statements because each contribution is model-specific.

**Signal-weak application?** no

**What was preserved verbatim:**
- All four contribution claims.
- POIs, official spatial databases, and published studies retained as originally stated.

### Reusability Assessment

**Worth generalizing?** YES

- **Rule candidate:** "For IJPE model papers, contribution lists should name the decision object and the model mechanism rather than using generic contribution language."
- **Condition:** Model-based production/supply-chain introduction.
- **Target skill:** this-journal-only
- **Evidence strength:** consistent with corpus contribution patterns

## Aggregated Rule Candidates

| Entry ID | Rule Candidate | Target Skill | Human Decision |
|----------|----------------|--------------|----------------|
| introduction-para-2 | "Name the operational decision and the coordination incentives it reallocates before presenting the formal model." | journal-adaptive-general | pending |
| introduction-para-3 | "End the introduction gap paragraph by naming the exact decision bundle the model resolves." | journal-adaptive-general | pending |
| introduction-para-7 | "For IJPE model papers, contribution lists should name the decision object and the model mechanism." | this-journal-only | pending |

## Section Summary

**Journal match score — before revision:** 4.1  
**Journal match score — after revision:** 4.7

**Key patterns improved:**
- Ownership is framed more explicitly as a production and supply-chain design decision.
- The gap now names ownership, contract design, and lifecycle responsibility as a linked decision bundle.
- Contribution wording is more IJPE-specific and less generic.

**Remaining issues:**
- The corpus strongly supports explicit RQs and contributions, but final acceptance should be paragraph-level human reviewed.
