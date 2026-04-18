# program.md — B_Q05 HMC power

(Karpathy `autoresearch` pattern adaptation.)

## Objective

Produce a **power table**: at N subjects × T trials per subject in
the current design (N ≈ 30, T ≈ 700, single sensory-noise level,
two mirror-skew priors), report expected 95% credible-interval
widths for (i) group-mean Weber fraction, (ii) group-mean α, (iii)
per-subject σ_e, (iv) per-subject subjective-prior parameters
under partial-veridical relaxations.

Subsumes Q02 (subject-conditional bands): power analysis
naturally produces subject-level posterior-width estimates.

## Modify

- `branches/B_Q05_hmc_power/round0*.md`.
- `branches/B_Q05_hmc_power/README.md` cross-branch pointers.
- If synthesis accepts: one amendment paragraph in
  `boec_simulator/README.md` §Identifiability guarantees and
  sample-size floor, promoting "hierarchical HMC with partial
  pooling is the realistic tool" from a qualitative claim to a
  quantitative floor.

## Leave alone

- §Parametric commitments, Bundle B, §Meta-framework commitment.
- HMC implementation details (this branch specifies requirements,
  does not implement).
- Hahn-Wang-Wei 2025 Theorem 3 proof and its closure logic.

## Evaluation criterion

**Accept** iff:
- Power table produced with ≥ 2 literature-anchored effect-size
  estimates for each identifiability target.
- Each 95% CI width has a traceable derivation (Manning et al.
  2022 eNeuro; Hahn-Wei 2024 empirical CI widths; Acerbi 2012
  published posteriors).
- Delta-check passes.

**Reject otherwise**.

## Failure handling

- If the HWW 2025 Theorem 3 identifiability guarantee demonstrably
  does not transfer (single-noise-level data) → power table
  emphasises group-level identifiability only; subject-level
  entries marked "broad posterior; not identifiable per-subject
  without multi-noise data".
- If no literature anchors exist for a target (e.g., subjective-
  prior skew parameter under veridical-relaxation) → admit and
  flag as "requires synthetic simulation — deferred to
  simulator-code task Q01/Q06".

## No help

Runs within 5-round cap autonomously.

## Budget

- Round 1: literature review — published HMC posterior widths in
  timing observer fits.
- Round 2: generator-side persona — synthetic-data spec (which
  cells at which α values are the benchmarks).
- Round 3: verifier-side persona — expected posterior-width
  estimates under hierarchical HMC.
- Round 4: power table assembly; cross-check against B_Q09.
- Round 5: decision — is the current design adequately powered?
  If not, how many more (subjects × trials)?

## Karpathy delta check

> **Delta**: [§Identifiability floor gains / loses: \<content\>,
> ≥ n quantitative citations, ≥ m posterior-width numbers.]

If `n < 2` AND `m = 0`: branch early-exits.
