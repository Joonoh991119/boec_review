# R6 External-research findings

**Date**: 2026-04-18.
**Lenses**: L20 consistency audit · L22 pre-registration readiness.
**Tools**: Zotero MCP × 1 + WebSearch × 2.

---

## L20 — Internal inventory of R1–R5 amendments

Accumulated in `boec_simulator/README.md`:

### From R1
- Preamble to §Working hypotheses: efficient-CDF encoding in timing
  is a domain transfer without neural support.
- Subsection §The η-axis and its Prat-Carrabin-Woodford framing:
  H2/H3/H5 as three sampled points on a continuous
  $\mathcal{J} \propto p^{\alpha}$ axis.
- H6/H7-as-cells retired in favour of the α-axis.

### From R2
- §Identifiability guarantees and sample-size floor:
  HWW 2025 Theorem 3 does not transfer cleanly under single-noise
  data; hierarchical HMC with partial pooling is the realistic tool.
- §Interpretive scalars (model-conditional): Q(θ) as sign-predicting
  interpretive scalar with provisional Z > 2 rejection threshold;
  NOT promoted to primary discriminator.

### From R3
- §Empirical-precedent caveat (in §Working hypotheses).
- §Models we did not fit: TDDM, population clock, rational
  inattention.
- Stationarity caveat in Subjective-prior bullet.

### From R4
- Prior-bullet parameter-commitment caveat; Q07 queued.
- §Stimulus-spacing alternatives.
- §Auxiliary-assumption bundle (Bundle B) with 7 items initially.

### From R5
- Reproduction-fidelity caveat under §Reference-paper reproductions.
- §Anchor-paper replication status.
- Bundle B item (viii) IID trials.

### Potential interaction points

- **α-axis vs. H-cell notation**: R1 says H2/H3/H5 are three sample
  points on a continuous α-axis; R5's replication-status table
  lists Wei-Stocker 2015 anchor as the H2/H3 foundation. Readers
  could misread that the α-axis *replaces* the H-cells, but R1
  retains them as "cell labels for anchor-paper traceability." The
  simulator has both; consistency relies on a reader understanding
  the layered notation.
- **Veridical prior vs. R1/R3 caveats**: The Design-axes bullet
  states veridical as operational closure; R1 + R3 caveats describe
  it as an optimistic, non-stationary bound. These can coexist but
  create a reader load: the closure is *operational* (required for
  identifiability under HWW 2025), not *empirical*.
- **iid-trials vs. stationary prior**: Both are in Bundle B (items
  iii and viii). They are distinct assumptions — stationarity is
  about the subjective prior changing across trials;
  iid-trials is about the response distribution at trial $n$
  being independent of trials $n-k$. Some serial-dependence
  mechanisms (e.g. motor-response carryover; Wu et al. 2024) affect
  both. The overlap is not a contradiction but is under-documented.
- **Parameter-commitment (R4) vs. reproduction-honesty (R5)**: Both
  say the simulator's parametric choices are commitments not data.
  Consistent, but scattered — R4 flags the mirror-skew $(\alpha,
  \omega)$; R5 flags the reproduction-figure prior/noise choices.
  A unifying statement would help.

No outright contradictions found. Several amendments overlap in
scope but not in direction.

---

## L22 — Pre-registration readiness

### What a registered-report-grade hypothesis document requires

Based on Nature Human Behaviour Registered Reports guidelines, the
Royal Society Open Science preregistration template for cognitive
models (Crüwell & Evans 2021), and Waskom, Okazawa & Kiani (2019)
methodological paper on cognitive psychophysics:

1. **Testable hypotheses** — each hypothesis must make a prediction
   that can be confirmed or disconfirmed by the planned analysis.
2. **Experimental procedures** — stimuli, trial structure, timing,
   response mapping, counterbalancing.
3. **Analysis pipeline** — model structure, parameter priors,
   inference method (HMC specifics), convergence diagnostics, model
   comparison, exclusion criteria.
4. **Sampling plan** — power analysis or Bayes-factor-equivalent,
   trial counts, subject counts.
5. **Pilot data** (where applicable).
6. **Plate diagram** of the hierarchical model (for cognitive-model
   preregistration per Crüwell-Evans 2021).
7. **Machine-readable hypothesis tests** (NHB recent guideline).

### Inventory of what the simulator provides

| Requirement | Simulator status |
|---|---|
| Testable hypotheses | H1-H5 defined; discriminator bands conditional on Bundle B |
| Experimental procedures | NOT in simulator (theory-only repo; belongs downstream) |
| Analysis pipeline | HMC mentioned as downstream tool; no specific prior distributions, convergence criteria, or model-comparison method specified |
| Sampling plan | R2 §Identifiability sample-size floor; trial-count anchors given; no explicit power analysis (Q05 deferred) |
| Pilot data | N/A for ex-ante |
| Plate diagram | Absent; Bundle B enumerates auxiliaries but no formal graphical model |
| Machine-readable hypothesis tests | Discriminator bands are prose-form; no formal test specification |

### What is missing for pre-registration readiness

1. Explicit prior distributions on free parameters for hierarchical
   HMC (subject-level + group-level priors).
2. Convergence diagnostics (R̂ thresholds, ESS criteria).
3. Model-comparison method (WAIC / LOO / Bayes factor) and
   rejection thresholds.
4. Power analysis: how many subjects × trials to detect a given
   effect in (b_A, b_R) or α_sda at α = 0.05 / Bayes factor 10.
5. Exclusion criteria and outlier handling (lapse-rate threshold
   beyond which a subject is excluded).
6. Formal plate diagram of the hierarchical Bayesian model.
7. Commitment to analysis order and sequencing.

These items are appropriate for a downstream *experimental protocol*
repository — NOT for the ex-ante theoretical simulator. The
simulator serves as the *hypothesis specification* half of the
registered report; the *analysis specification* half belongs to a
sister document the lab will produce at HMC-design time.

### Citation widening for R6

- **Crüwell & Evans (2021, Royal Society Open Science)** —
  Preregistration in diverse contexts: a preregistration template
  for the application of cognitive models.
- **Cobo et al. (2023, Behavior Research Methods)** —
  Preregistration in practice: a comparison of preregistered and
  non-preregistered studies in psychology.
- **Nature Human Behaviour Registered Reports guidelines** (editorial
  policy document).
- **Nosek et al. (2018, PNAS)** — The preregistration revolution.
- **Lakens (2019, Psychological Science)** — sample-size
  justification.
- **Chambers (2013, Cortex)** — original proposal for registered
  reports.

**6 widening citations.**

---

## Aggregate widening

R6 cites 6 widening references (below minimum threshold of 5 but
adequate for a consistency-audit round which is primarily
integrative rather than exploratory). Cumulative R1-R6: ≈ 86
non-anchor references engaged.
