# R4 Synthesis

**Inputs**: `references/R04_findings.md`, `rounds/R04_critique.md`.

---

## Popper — parameter-space robustness band (L08)

**Decision**: **ACCEPT**. The mirror-skew design parameters are
commitments, not data. Robustness must be declared.

**Simulator amendments**:

1. In §Design axes and closures, reframe the Prior bullet:
   "The experimental prior is fixed to (α = ±3.3, ω = 0.3374). This
   is a parameter commitment inherited from p1_make_base_config.m
   defaults, not a theoretical prescription. All discriminator
   bands below are conditional on this choice. A prior-sensitivity
   sweep over α ∈ [±1.5, ±5.0] and ω ∈ [0.15, 0.40] is on the
   roadmap (open question Q07)."

2. New subsection §Stimulus-spacing alternatives (under Design
   axes): "The current θ-grid is linear-uniform. Log-uniform
   spacing would break the H1 ↔ H4 degeneracy the simulator
   currently flags as unresolvable. A confirmatory study should
   run a subset of subjects under log-uniform spacing; until then,
   H1 and H4 remain a single equivalence class."

**Deferred as Q07**: the actual sensitivity sweep requires running
the simulator under the (α, ω) lattice and re-rendering
bias/SD/α_sda predictions. That is simulator-code work — out of
scope for the theoretical loop.

---

## Quine — Bundle declaration block (L10)

**Decision**: **ACCEPT**. The seven auxiliaries are already
documented across multiple README sections but never consolidated.

**Simulator amendment**: consolidate the seven auxiliaries into a
single block at the head of the Discriminating-observables section,
titled "§Auxiliary-assumption bundle". Each of the seven is a
one-line statement with a literature anchor and the prior round
(R1/R2/R3) that audited it. Any future round adding an auxiliary
(e.g. multiplicative noise, Q(θ) auxiliary) extends this block.

Example format:

> **Bundle B** (the auxiliaries this simulator implicitly accepts):
> (i) Gaussian encoding noise in m-space (Wei-Stocker 2016;
> behavioural-level support: Keemink et al. 2018 / Park-Pillow 2024
> / Prat-Carrabin-Harl-Gershman 2026).
> (ii) Veridical subjective prior (Acerbi 2012; R1 caveat).
> (iii) Stationary prior (R3 caveat).
> (iv) Additive Gaussian motor noise only (HWW 2025 §2.5).
> (v) No lapse rate (standard omission; R4 caveat).
> (vi) BLS / L² readout (Jazayeri-Shadlen 2010; R2 caveat).
> (vii) Additive δ on f(θ) (small-noise approximation;
> Harris-Wolpert 1998 for multiplicative alternative).

---

## Fool — cite behavioural Gaussian justification (L10)

**Decision**: **ACCEPT** in part. Add citations for the Gaussian
behavioural-noise defence. **DEFER** the skewness-threshold
proposal (|γ| > 0.5 as a bundle-violation falsifier) — that
requires empirical calibration.

**Simulator amendment**: in the Bundle B item (i) above, append the
three citations (Keemink 2018, Park-Pillow 2024,
Prat-Carrabin-Harl-Gershman 2026) explicitly. Note that the
Gaussian assumption "derives behaviour-level support from
population-code literature showing recurrent-network Poisson
activity decodes to approximately-Gaussian behavioural noise
distributions."

**Deferred** (Q08): the skewness-threshold response-distribution
auxiliary violation band. Requires pilot data to calibrate.

---

## Summary of R4 amendments

### Accepted (applied to boec_simulator in parallel commit)

1. §Design axes and closures Prior bullet — reframe as parameter
   commitment, link to Q07.
2. New §Stimulus-spacing alternatives — log-uniform to break H1↔H4.
3. New §Auxiliary-assumption bundle (Bundle B) — seven items
   consolidated with round-of-origin tags and literature anchors.

### Deferred (open questions)

- **Q07** — prior-parameter sensitivity sweep (α × ω lattice).
  Simulator code task.
- **Q08** — response-skewness auxiliary-violation threshold |γ|.
  Requires pilot data.

### Retired lenses

- L08, L10 move to Completed.

### Widening audit

R4 cited **16 non-anchor refs**: Manning et al. 2022, Depaoli-Winter-
Visser 2020, Sridharan-Castiglione 2014, Hedges et al. 2011,
Sotiropoulos et al. 2014, Jogan & Stocker 2015, Wichmann-Hill 2001,
Acerbi-Vijayakumar-Wolpert 2014, Shih-Tang 2023, Harris-Wolpert
1998, Keemink-Tailor-van Rossum 2018, Park-Pillow 2024,
Ma-Beck-Latham-Pouget 2006, Prat-Carrabin-Harl-Gershman 2026,
Tessari et al. 2024, Luu-Stocker-Donner 2018.

### Next round (R5)

Active backlog remaining: L09 reference-paper reproduction
honesty, L15 confounders in mirror-skew, L18 replication status
of 8 anchors.

R5 should take L09 + L18. These are audit lenses that extend the
widening-against-anchor-overfit discipline — L09 checks that the
simulator's reproduction figures don't silently re-parametrise the
anchors; L18 checks whether any anchor has been independently
replicated or challenged.
