# R2 External-research findings

**Date**: 2026-04-18.
**Lenses**: L07 (identifiability proofs vs. practical sample size),
L14 (Hahn-Wei 2022 P/P ratio Q(θ) as a primary discriminator).
**Tools**: Zotero MCP × 3 semantic queries, WebSearch × 3.

---

## L07 — Identifiability vs. practical sample size

### Governing theorem
**Hahn, Wang & Wei (2025)** Theorem 3: "the components of Bayesian
observer models are usually identifiable if response distributions
based on *multiple small sensory noise levels* and a sufficiently
large number of trials are available … the reason enabling this
identifiability with multiple sensory noise levels lies in the
second-order, nonlinear scaling of the bias with the magnitude of
the sensory noise." The guarantee is *conditional on multi-noise*
data, not single-noise data.

### Transfer to the mirror-skew timing design
The current design has two priors (mirror-skew) but **one effective
sensory-noise level per subject** (each subject's internal timing
noise is a fixed, unknown parameter). The HWW 2025 guarantee does
NOT transfer cleanly:

- Their "multiple small sensory noise levels" require an
  experimental manipulation of noise (contrast, presentation time,
  stimulus ambiguity). Duration-reproduction tasks typically cannot
  vary the internal noise directly; any manipulation (e.g., shorter
  flash, faster encoding window) changes stimulus parameters rather
  than σ_internal.
- The mirror-skew prior does provide a different identifiability-
  breaking covariate (prior shape), which HWW 2025 §2.4 discusses
  as the "multi-context adaptation" escape for the exceptional
  Weber + log-prior degenerate case. But this escape is only
  guaranteed when both encoding AND subjective prior adapt; if only
  the subjective prior adapts across conditions (the likely case in
  a short duration experiment), the escape is partial.

### Empirical sample-size baselines
- **Acerbi, Wolpert & Vijayakumar (2012)** — duration reproduction,
  **≈2,700 trials per subject** for a full Bayesian observer factorial
  model comparison.
- **Sohn & Lee (2013)** — 9 durations × 30 trials × 10 sessions =
  2,700 trials per subject; Bayesian observer with three free
  parameters.
- **Hahn-Wei 2024 (published Nat. Neurosci. version of 2022 preprint)**
  — fits six datasets with trial counts ranging 800-10,000 per
  subject; uses mixture-of-Gaussians priors and analytical
  bias/SD formulas.
- **Manning et al. (2023, eNeuro)** — "A general framework for
  inferring Bayesian ideal observer models from psychophysical data"
  — parameterises arbitrary prior shapes using mixtures of Gaussians,
  produces analytical solution for psychophysical quantities.
  Recommends ≥ 500 trials per subject per condition for stable prior
  recovery.
- **Acerbi & Ma (2017)** — Bayesian Adaptive Direct Search (BADS) for
  observer-model fitting with up to 6 free parameters; typical
  psychophysics trial counts are sufficient *if* the model is
  well-specified.

### Hierarchical Bayesian fitting as the practical bridge
When per-subject trial counts are modest, hierarchical Bayesian
models partially pool information across subjects:
- **Dunovan, Tremel & Wheeler (2014)** — hierarchical drift-diffusion
  with group-level and subject-level estimates.
- **Park (2025)** — hierarchical Bayesian serial-bias modelling;
  sample-size planning done frequentist but inference via HMC.
- Emerging consensus: HMC / NUTS is the de facto fitting tool for
  moderately complex observer models; STAN / PyMC implementations
  routinely converge for 200–400 subject-level parameters.

### The practical identifiability gap for this project
Given the current design (2 priors × ≈ 700 trials × ≈ 30 subjects
realistically), the HWW 2025 Theorem 3 guarantee does not formally
apply. The simulator must warn the HMC user that:

1. Individual parameters (per-subject $\sigma_e$, effective
   subjective prior) are only identifiable under the explicit
   closure assumptions (veridical prior, BLS loss). If those fail,
   posteriors on individual parameters will be broad.
2. Population-level parameters (group means of $w$, $\sigma_0$,
   $\eta$, or the unified $\alpha$) can be identified under
   hierarchical pooling even at modest per-subject counts — this is
   the realistic inferential target.
3. Model-comparison claims (H1 vs H2, H2 vs H3) should be made at
   the group level, not per-subject; per-subject WAIC differences
   typically overlap.

---

## L14 — Hahn-Wei Q(θ) ratio as a discriminator

### Definition
Hahn & Wei (2022 preprint → 2024 Nat. Neurosci.) Equation 4:
$$
Q(\theta) \;=\; \frac{d}{d\theta}\!\left[\,\frac{p_{\mathrm{prior}}(\theta)}{\mathcal{J}(\theta)^{(p+2)/4}}\right].
$$
The sign of Q(θ) predicts the sign of the bias at θ. For BLS
($p = 2$) the exponent is $(p+2)/4 = 1$, so
$Q(\theta) = \partial_\theta [p_{\mathrm{prior}}(\theta) / \mathcal{J}(\theta)]$.
**Q(θ) encodes the competition between prior slope and Fisher-
information slope**: when the prior changes faster, attraction
wins; when the encoding precision changes faster, repulsion wins.

### Published validation
Hahn-Wei 2024 Nat. Neurosci. Fig. 7a: across six datasets
(orientation × 3, direction, colour, time, numerosity) the ratio
rule correctly predicts the bias sign at the majority of stimuli.
Fig. 7b: repulsion is larger in the four **circular** datasets and
smaller in the two **scalar** datasets (numerosity, time). In time
and numerosity, **prior attraction dominates**. Direct quote:
"repulsive biases play a larger role in accounting for the overall
biases in the four circular datasets, and a smaller role in the two
scalar datasets."

### Relevance to the simulator
1. Q(θ) is a *sign-only* discriminator. It tells you whether bias is
   attractive or repulsive at each θ but not by how much. α_sda (the
   log-SD slope) remains necessary for magnitude/strength of
   BOEC-family inflation. The two observables are complementary.

2. For the mirror-skew timing design, the H-W 2024 result predicts
   **attractive Q(θ) dominates** in timing even under a BOEC-family
   observer — because the prior ($\omega \approx 0.3374$, compact)
   changes faster than the Fisher-information term ($\mathcal{J} \propto
   p^{\alpha}$, which also reflects the same prior). This flips the
   simulator's current claim that H2 / H3 / H5 produce "repulsive
   bias signatures" in timing: the actual repulsive direction is a
   feature of the asymmetric $\theta$-space likelihood near the
   prior mode, not of the overall bias at all θ.

3. **Key amendment candidate**: the simulator currently states bias
   sign at θ = 1.1 as the primary discriminator, but Q(θ) predicts
   that the SIGN FLIP between H1/H4 and H2/H3/H5 is not just at θ =
   1.1 but is a function that varies across θ. A better discriminator
   is: **the integral or integrated-sign of Q(θ) across the
   experimental θ range**, weighted by the experimental prior. That
   is one scalar per subject and is model-family-diagnostic without
   cherry-picking a single probe.

### Cross-connection to R1 α-axis
The α-axis re-framing from R1 maps directly onto Q(θ):
$\mathcal{J} \propto p^{\alpha}$ gives
$\mathcal{J}^{(p+2)/4} \propto p^{\alpha(p+2)/4}$, so
$$
Q(\theta) \;=\; \partial_\theta\!\left[\,p(\theta)^{\,1 - \alpha(p+2)/4}\,\right].
$$
Under BLS ($p = 2$): exponent is $1 - \alpha/2$. When $\alpha = 2$
(H2) the exponent is 0 — Q(θ) vanishes and the bias sign is
neutral (tied between attraction and repulsion at every θ). When
$\alpha > 2$ (H3 with $\eta > 0$) the exponent is negative,
repulsion dominates. When $\alpha < 2$ (including $\alpha = 0$, the
prior-only null) the exponent is positive, attraction dominates.

Q(θ) is therefore the *α-derivative* of the bias sign — the cleaner
parameterisation of the same discriminator.

---

## Papers newly surfaced this round

- **Manning, Prat-Carrabin & Woodford (2023)** — eNeuro — "A general
  framework for inferring Bayesian ideal observer models from
  psychophysical data." Mixture-of-Gaussians priors with analytical
  psychophysical solutions; highly relevant to HMC implementation.
- **Bévalot & Meyniel (2023)** — "A dissociation between the use of
  implicit and explicit priors in perceptual inference." Explicit
  identifiability verification via recoverability checks —
  methodological template.
- **Acerbi & Ma (2017)** — BADS optimiser for observer-model
  fitting. Standard tool in this literature.
- **Park (2025)**, **Dunovan et al. (2014)** — hierarchical HMC
  templates.
- **Fritsche, Spaak & De Lange (2020)** (second mention, different
  relevance) — concurrent attractive and repulsive history biases;
  eLife 2020.
- **Moon & Kwon (2022)**, **Cheng, Chen & Shi (2024)** — attractive
  and repulsive biases coexist; direction vs time show opposite net
  biases, matching the Hahn-Wei 2024 scalar-vs-circular finding.

---

## K-Dense Web prompt for user

Recommend launching at [www.k-dense.ai](https://www.k-dense.ai):

> For a duration-reproduction psychophysics experiment with two
> mirror-skew priors (α = ±3.3) and no sensory-noise manipulation,
> what is the sample-size floor (trials × subjects) at which a
> hierarchical Bayesian observer model with 6–10 parameters per
> subject can recover (i) group-mean Weber fraction, (ii) group-mean
> efficient-coding strength α, (iii) per-subject posterior ranges,
> all at > 0.95 coverage? Compare against Acerbi 2012 (2,700
> trials/subject, 5 subjects), Sohn-Lee 2013 (2,700 × 6), Hahn-Wei
> 2024 (up to 10,000 × small cohorts). Include the identifiability
> corollary from Hahn-Wang-Wei 2025 Theorem 3 on multi-noise-level
> data.

---

## Integrated conclusion

R2 supports two simulator amendments:

1. **Add a §"Identifiability guarantees and sample-size floor"**
   that states: HWW 2025 Theorem 3 requires multi-noise-level data;
   the current design substitutes multi-prior-shape for multi-noise
   (partial escape); population-level inference is the realistic
   target, not per-subject.

2. **Promote Q(θ) to a secondary discriminator alongside α_sda** in
   the §Discriminating observables table. Report an integrated-Q
   scalar per subject; the integrated sign predicts
   attractive-vs-repulsive family membership more honestly than a
   single-probe bias sign at θ = 1.1.
