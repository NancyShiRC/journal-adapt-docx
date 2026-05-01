# Simulation / Results — Mode C Fast Scan

Overall match: 3/5

Issues above LOW severity:

1. **Table integrity.** Tables 3-5 and appendix tables are corrupted in the converted Markdown. This is a conversion artifact, but it is submission-critical because the tables currently contain broken words, merged cells, and misplaced symbols.
2. **Calibration boundary.** The prose correctly states that the simulations are not causal estimation. Preserve this boundary throughout all results paragraphs.
3. **Mechanism labeling.** When reporting scenario results, make every comparison follow the IJPE sequence: ownership structure -> mechanism -> implication. Avoid listing rankings without explaining whether the driver is lifecycle cost, service investment, double marginalization, or recovery responsibility.

Recommendation: targeted prose cleanup only; do not rewrite equations, numerical results, figures, or tables until the source tables are reconstructed.

## Replacement Calibration Frame

Use this paragraph at the start of Section 4 if a more compact framing is desired:

The simulations use observed spatial data to discipline market scale and service-level heterogeneity, while treating private tariffs, contract terms, and owner-specific lifecycle costs as transparent scenario parameters. The purpose is not to estimate a single empirical equilibrium. Instead, the simulation design evaluates how ownership and contract preferences change across mature dense markets, high-demand underserved markets, and expansion-market service gaps.

## Result-Narration Rule for Section 4

Each results paragraph should use this order:

1. State which structure or scenario performs better.
2. Identify the mechanism: lifecycle-cost advantage, service-level incentive, double marginalization, residual-value capture, or platform coordination.
3. State the bounded implication for ownership or contract design.
4. Avoid causal language unless the claim follows directly from the model.
