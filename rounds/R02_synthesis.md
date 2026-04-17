# R2 Synthesis

**Inputs**: `references/R02_findings.md`, `rounds/R02_critique.md`.
**Decisions**: accept / reject / defer per critique point.

---

## Hahn — identifiability transfer is conditional (L07)

**Decision**: **ACCEPT**. HWW 2025 Theorem 3 requires multi-noise-level
data; the mirror-skew duration design is multi-prior-shape data, which
is a partial escape and only for the exceptional degeneracy cases. The
simulator currently leans on the theorem without stating this.

**Simulator amendment**: add §"Identifiability guarantees and sample-
size floor" immediately after §"Interpretation guardrails". State:

1. HWW 2025 Theorem 3 requires multiple sensory-noise levels. The
   present design has one effective internal noise per subject.
2. Multi-prior-shape data provides a partial identifiability escape
   (HWW 2025 §2.4), but only for cases where both encoding *and*
   subjective prior adapt between contexts — a stronger condition
   than typically met in short duration experiments.
3. At realistic sample sizes (≈ 700 trials × ≈ 30 subjects),
   hierarchical HMC with partial pooling is the practical inference
   tool. Group-level parameters (mean Weber fraction, mean α)
   identify tightly; per-subject parameters have broader posteriors.
4. Acerbi 2012 (≈ 2,700 trials × 5 subjects), Sohn-Lee 2013
   (≈ 2,700 × 6), Manning-Prat-Carrabin-Woodford 2023 (≥ 500 /
   subject / condition), Hahn-Wei 2024 (up to 10,000) anchor the
   trial-count floor.
5. Model-comparison claims (e.g. H1 vs. H3) must be made at the
   group level; per-subject WAIC differences typically overlap.

---

## Quine — bundle declaration for Q(θ) (L14)

**Decision**: **ACCEPT in part**. Q(θ) is a model-conditional summary
statistic, not a model-free observable. If promoted, the simulator
must declare the auxiliary bundle.

**Simulator amendment**: if Q(θ) is added to Discriminating observables
(conditional on Popper's rejection-threshold concern being addressed
below), the row must cite the bundle explicitly:

> "Q(θ) integral assumes: Gaussian encoding noise in m-space,
> veridical subjective prior (R1 caveat), stationary prior (no
> trial-by-trial adaptation), BLS / L² readout, no motor noise. Each
> assumption is an open question (Q01-Q03) whose failure can flip the
> observed sign."

Rejected sub-claim: Quine's stronger demand that Q(θ) be retired
entirely — rejected because the α-axis from R1 maps algebraically
onto Q(θ) (R2 findings §L14 cross-connection), making Q(θ) the same
one-parameter family, not a separate commitment.

---

## Popper — rejection thresholds or demotion (L14)

**Decision**: **ACCEPT**. Without a rejection threshold, Q(θ) cannot
be a primary discriminator. It can be a secondary interpretive
scalar, but must not sit next to α_sda as a falsifier.

**Simulator amendment**:

- Do NOT promote Q(θ) to the Discriminating observables table.
- Add a separate paragraph under the table titled "Interpretive
  scalars (model-conditional)" listing Q-integral and any other
  derived quantities. Explicitly warn that Hahn-Wei 2024 Fig. 7
  predicts attraction-dominant Q-integral in time-domain data; the
  simulator's BOEC-family predictions ask the data to contradict this
  pattern, which is an implicit falsification condition that must be
  stated explicitly before data collection.
- Commit a provisional threshold: "A group-level Q-integral Z > +2
  in either prior condition rejects the BOEC-family hypothesis
  (H2/H3/H5) in favour of the classical family (H1/H4)." This is a
  falsifier — now the simulator has one for Q(θ).

---

## Summary of R2 outcomes

### Accepted simulator amendments (applied in parallel commit)

1. New §"Identifiability guarantees and sample-size floor" after
   §"Interpretation guardrails". HWW 2025 Theorem 3 caveat, sample-
   size anchors, hierarchical group-level inference as the realistic
   target.
2. New paragraph "Interpretive scalars (model-conditional)" under
   the Discriminating observables table. Q-integral listed with
   auxiliary bundle and provisional rejection threshold. Q(θ) NOT
   promoted to the primary table.

Cross-reference: this synthesis document.

### Deferred (filed as open questions)

- **Q04** — the Q-integral rejection threshold (+2 Z) is provisional;
  a sweep over the null distribution under each auxiliary-failure
  mode would tighten it. Defer to a round that picks up the
  generative-model assumption audit (L10).
- **Q05** — a hierarchical-HMC sample-size / power simulation under
  the current design parameters would quantify the per-subject
  posterior breadth and confirm the group-level identifiability claim.
  Defer.

### Retired lenses

- L07, L14 moved to "Completed" in LENSES.md.

### Methodological reflection

This round integrated six references outside the 8-anchor core
(Manning et al. 2023, Bévalot & Meyniel 2023, Acerbi & Ma 2017,
Park 2025, Dunovan et al. 2014, Fritsche et al. 2020 second
relevance). The loop's rule is to widen the bibliography with each
round to prevent anchor-paper overfit.

### Next round (R3)

Candidates from the active backlog: L08 (experimental-parameter
sensitivity), L09 (reference-paper reproduction honesty), L10
(generative-model assumption audit), L11 (empirical precedent for
efficient-CDF in timing), L12 (alternative observer frameworks),
L13 (prior-learning dynamics), L15 (confounders in mirror-skew).

R3 should prioritise L11 (empirical precedent for efficient-CDF in
timing) and L12 (alternative observer frameworks) — both continue
the widening against anchor-paper overfit. L13 (prior-learning
dynamics) pairs naturally with both.
