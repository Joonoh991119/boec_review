# B_Q05 — Hierarchical HMC power-analysis branch

**Parent question (from main loop)**: Q05 — under the current design
(≈ 30 subjects × 700 trials, mirror-skew priors, single effective
sensory-noise level per subject), quantify posterior-width
expectations for (i) group-mean Weber fraction, (ii) group-mean
α (efficient-coding strength), (iii) per-subject σ_e, (iv)
subjective-prior parameters under partial-veridical relaxations.

Subsumes Q02 (subject-conditional discriminator bands): any power
analysis produces subject-level posteriors that naturally yield
the subject-conditional bands Popper demanded in R4.

**Harness pattern**: generate-and-verify.
- **Generate**: synthetic-data agent produces hierarchical datasets
  drawn from each H in {H1, H2, H3, H4, H5} at α ∈ {0, 1, 2, 3}.
- **Verify**: HMC-fit agent runs a hierarchical Bayesian model on
  each dataset and reports posterior credible-interval widths for
  each identifiability target.

## Scope

**In scope**:
- Theoretical power estimates based on Hahn-Wang-Wei 2025
  identifiability results under multi-prior-shape (not multi-noise)
  data.
- Literature-derived effect-size anchors for α_sda and
  (b_A, b_R) sign contrast at (α = ±3.3, ω = 0.34).
- Subject-level posterior-width expectations.

**Out of scope**:
- Actually running synthetic HMC simulations — simulator-code task.
  This branch produces the specification of what a simulation
  should check, not the simulation itself.
- Multi-noise-level identifiability (would require adding noise
  manipulation to the design — separate experiment).

## Round plan (capped at 5)

| Round | Focus | Deliverable |
|---|---|---|
| B5R1 | Literature review: empirical effect-size anchors | `round01_findings.md` |
| B5R2 | Generator-side persona: synthetic-data specification for each cell at various α | `round02_generator_spec.md` |
| B5R3 | Verifier-side persona: HMC posterior-width estimates under HWW 2025 Theorem 3 partial-transfer | `round03_verifier_spec.md` |
| B5R4 | Power table: at N subjects × T trials, group-mean α 95% CI width expected to be ± x | `round04_power_table.md` |
| B5R5 | Decision: is the current design adequately powered? If not, how many more subjects/trials required? | `round05_decision.md` |

## K-Dense prompt

See `k_dense_prompt.md`.

## Cross-branch pointers

- B_Q09 status: _pending_
- B_Q06 status: _pending_
