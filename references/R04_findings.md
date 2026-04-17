# R4 External-research findings

**Date**: 2026-04-18.
**Lenses**: L08 experimental-parameter sensitivity · L10 generative-model
assumption audit.
**Tools**: Zotero MCP × 3 + WebSearch × 3.
**Widening audit**: ≥ 5 non-anchor refs per lens.

---

## L08 — Experimental-parameter sensitivity

### Prior parameter sweep

The mirror-skew α = ±3.3, ω = 0.3374 choice inherits from
`p1_make_base_config.m` defaults. No published paper defends this
specific combination for interval timing. A principled sensitivity
sweep should consider:

1. **Smaller |α|** (e.g. ±1.5) — the skew becomes less extreme; the
   asymmetry in the $\theta$-space likelihood under efficient-CDF
   weakens. When $|\alpha| \to 0$ the prior is Gaussian and the
   skew-induced BOEC signature disappears.
2. **Larger |α|** (e.g. ±5) — larger skew, stronger BOEC signature,
   but tails become extremely thin and the mirror overlap at
   θ = 1.1 shrinks. Statistical power on the shared probe drops.
3. **Smaller ω** (narrower prior) — more compact mass, faster
   prior changes, stronger prior-attraction contribution per
   Hahn-Wei Q(θ). Shifts the attraction/repulsion balance.
4. **Larger ω** (wider prior) — broader mass, more effective subjects
   but less shape information.
5. **Multimodal priors** — not mirror-skew at all; Hahn-Wei 2022 shows
   bimodal priors produce qualitatively different bias patterns.

**Findings from literature**:
- **Manning, Naecker, McLean, Rokers, Pillow & Cooper (2022, eNeuro)**
  — "A General Framework for Inferring Bayesian Ideal Observer Models
  from Psychophysical Data." Systematic approach to prior
  parameterisation: mixtures-of-Gaussians with free weights, means,
  variances. Explicit discussion of parameter recoverability as a
  function of stimulus range and sampling density.
- **Zhang & Stocker (2021)** — uses tightly-constrained observer
  models specifically because previous reverse-engineered priors
  "showed large variations across subjects, indicating a potential
  case of over-fitting due to insufficient model constraints
  (Stocker & Simoncelli 2006; Hedges et al. 2011; Sotiropoulos et
  al. 2014; Jogan & Stocker 2015)." Constraining the prior
  parametrically reduces overfit but locks in a prior-family
  commitment.
- **Depaoli, Winter & Visser (2020, Frontiers in Psychology)** —
  prior sensitivity analysis: systematic sweep over prior
  hyperparameters to check if posterior conclusions depend on prior
  choice. Should be applied to the simulator's α, ω, θ-range
  choices.
- **Sridharan & Castiglione (2014, Int. J. Approx. Reasoning)** —
  "Bayesian robustness under a skew-normal class of prior
  distribution." Global sensitivity analysis for skew-normal-class
  priors. Directly applicable to the mirror-skew design.

### Stimulus spacing

- **HWW 2025 §2.4**: multi-context adaptation escapes the
  exceptional degenerate cases only when BOTH encoding AND
  subjective prior change between contexts. Mirror-skew is one
  prior change; does it count as "context adaptation" in the
  HWW sense? Ambiguous — HWW used vision experiments with explicit
  contrast manipulation.
- **Log-uniform vs. linear-uniform stimulus spacing**: the
  simulator's θ-grid is linear. Log-uniform spacing would bias
  stimulus sampling toward short durations; this would change
  Jazayeri-Shadlen-style effective priors. **H4 (Fechner log) vs.
  H1 (linear Weber)** is degenerate under linear-uniform spacing;
  log-uniform spacing would break the degeneracy because H4 would
  reduce to constant noise in log-space while H1 would still have
  Weber-scaling noise.

**Refs outside 8-anchor**: Manning et al. 2022, Depaoli-Winter-Visser
2020, Sridharan-Castiglione 2014, Hedges et al. 2011, Sotiropoulos
et al. 2014, Jogan & Stocker 2015. **6 widening citations.**

---

## L10 — Generative-model assumption audit

### (i) Gaussian encoding noise in m-space

The simulator assumes $m = f(\theta) + \delta$, $\delta \sim
\mathcal{N}(0, \sigma_e(\theta)^2)$.

- **Wei & Stocker (2016, Neural Comput.)** prove that the
  efficient-coding Fisher-info-∝-prior result **requires effective
  noise to be Gaussian**. Non-Gaussian noise introduces a
  correction term $D_0$ that shifts the Fisher-MI relationship
  (the R5 correction in the simulator's existing analysis).
- **Keemink, Tailor & van Rossum (2018, Neural Comput.)** — in
  population-code simulations, "the shape of the bias curve and
  the distribution of estimates are very similar when, instead of
  gaussian noise, Poisson or multiplicative gaussian noise is
  considered." Good news: Gaussian is a reasonable approximation
  at the *bias* level.
- **Park & Pillow (2024, preprint)** — *Bayesian Efficient Coding* —
  Gaussian additive noise is analytically tractable; Poisson
  requires numerical optimisation. Different noise distributions
  lead to different optimal tuning curves.
- **Ma, Beck, Latham & Pouget (2006)** — probabilistic population
  codes (PPCs); Poisson-like variability gives rise to a
  Gaussian-in-stimulus-space likelihood under specific conditions.
- **Prat-Carrabin, Harl & Gershman (2026, preprint)** — *Fast
  efficient coding and sensory adaptation in gain-adaptive
  recurrent networks.* Recurrent networks give effective Gaussian
  noise at the decoded level even if the underlying spikes are
  Poisson. Supports the Gaussian-at-behaviour-level assumption.

**Assessment**: Gaussian encoding noise is a defensible first-order
approximation. The $D_0$ correction already handles mild
deviations. Full Poisson treatment would require switching to a
PPC formulation, out of scope.

### (ii) Motor noise

- **HWW 2025 §2.5** — *"Commonly considered motor noise in
  estimation tasks does not affect the identifiability."* Proof that
  symmetric additive motor noise separates from sensory noise given
  enough trials. **Good news**: simulator can safely omit motor
  noise from the bias/SD predictions at the ex-ante stage;
  motor-noise-related variance will be absorbed into the
  per-subject σ_e posterior without biasing α.
- **Luu, Stocker & Donner (2018, eLife)** — measured motor noise in
  a control experiment and used it in all subsequent fits. Standard
  practice.
- **Tessari, Hermus, Sugimoto-Dimitrova & Hogan (2024)** — argue
  motor noise may be signal-dependent (Harris-Wolpert 1998).
  Relevant if motor response amplitude correlates with produced
  interval.

**Assessment**: motor noise is safe to omit ex-ante but should be
measured and included at HMC stage.

### (iii) Lapse rate / attention lapses

- **Wichmann & Hill (2001, Perception)** — standard lapse-rate
  formulation: psychometric function asymptote deviates from 0/1
  by a lapse rate.
- **Acerbi, Vijayakumar & Wolpert (2014, PLoS Comput. Biol.)** —
  include a lapse parameter $\lambda \in [0, 1]$ in observer model;
  fit per-subject.
- **Shih & Tang (2023)** — online vigilance tasks show bias, lapse
  rate, and guess rate all change with time-on-task.

**Assessment**: the simulator currently omits lapses. This is a
first-order omission. Predicted bias/SD curves at high-noise
regimes will be softened by occasional lapses. Should be flagged.

### (iv) Signal-dependent vs. additive noise

Current σ_e(θ) is signal-dependent by construction in H1/H3/H5
(Weber or efficient-prior). But the noise is additive on f(θ), not
multiplicative on θ. This is a modelling choice; some literature
uses multiplicative noise directly.

- **Harris & Wolpert (1998, Nature)** — signal-dependent motor
  noise: variance grows with muscle command. Applies to the
  reproduction response.
- **Acerbi et al. 2012** — "scalar property" for time interval
  timing: variability grows linearly with magnitude, consistent
  with Weber-scaling implemented via additive-on-f approach.

**Assessment**: additive-on-f is a reasonable proxy for
multiplicative-on-θ in the small-noise regime. Should be
flagged as an approximation.

### (v) Stationarity of subjective prior

Already addressed in R3 L13.

### (vi) Loss function

Already addressed in R2 (closure to L²).

### (vii) Subjective prior = objective

Already addressed in R1 L04 and R3 L13.

**Refs outside 8-anchor**: Wichmann-Hill 2001, Acerbi-Vijayakumar-
Wolpert 2014, Shih-Tang 2023, Harris-Wolpert 1998, Keemink-Tailor-
van Rossum 2018, Park-Pillow 2024, Ma-Beck-Latham-Pouget 2006,
Prat-Carrabin-Harl-Gershman 2026, Tessari et al. 2024, Luu-Stocker-
Donner 2018. **10 widening citations.**

---

## Aggregate widening

16 refs outside the 8-anchor set this round. Cumulative across
R1-R4: **60+ non-anchor refs** engaged.

## K-Dense Web prompt for user

> Run a robustness sensitivity analysis on the mirror-skew
> α = ±3.3, ω = 0.3374 design. For each of α ∈ {1, 2, 3, 4, 5}
> and ω ∈ {0.1, 0.2, 0.3, 0.4}, compute the predicted (b_R, b_L)
> sign stability, the predicted α_sda range, and the expected
> within-subject power at 700 trials × 30 subjects to discriminate
> H1 vs. H3 at the group level. Report the sensitivity-robust
> subset of (α, ω) pairs that preserve H1-H5 separability. Include
> a log-uniform-spacing variant as a point of comparison.
