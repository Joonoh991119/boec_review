# R1 Critique — three personas

**Lenses**: L04 (design-prediction circularity), L05 (theoretical
coherence across refs), L06 (H6 / H7 candidate assessment).

**Personas deployed**: Popper (L04), Prat-Carrabin (L05), Ganguli (L06).

Each critique draws on `references/R01_findings.md`. Quotations are
from that document or from the papers it cites.

---

## Popper on L04 — Design-prediction circularity

The mirror-skew choice $\alpha = \pm 3.3$ is presented in the simulator
as an experimental constraint, but no paper in the anchor set defends
this specific value for timing tasks. The value was inherited from
`p1_make_base_config.m` defaults. That is a provenance, not a
justification — and provenance is not identifiability.

Three independent findings in R1 pull the prediction-design relationship
in the same direction. Luu, Stocker & Donner (2018) report that "all
subjects seemed to substantially overestimate the width of the stimulus
prior"; Roach et al. (2016) find "partial prior recalibration" with
indifference points falling toward the global mean; Acerbi et al. (2012)
recover heavy-tailed subjective priors even from compact experimental
priors. In the mirror-skew design, all three effects shift the
*effective* subjective prior toward a broader, less-skewed distribution
than the one the simulator assumes. The simulator's veridical-prior
predictions are therefore an **upper bound** on the BOEC signature the
data can show.

This is the strict Popperian concern: the simulator names what H2, H3,
H5 predict *if* subjects learn $\alpha = \pm 3.3$ faithfully, but the
relevant empirical question is whether *any* subject satisfies the
antecedent. If no subject does — a possibility all three findings
above make plausible — then the prediction is about a
counterfactual observer, not about the experimental subjects, and the
discriminator bands in the README are not actual rejection thresholds
for the experiment under consideration.

**Demand**: the simulator must state the subject-side condition under
which its discriminators would hold — "for subjects whose inferred
$|\alpha^{\mathrm{subj}}| > 2.5$ (say), $\alpha_{\mathrm{sda}} > 0.20$
rejects H2 in favour of H3 at η ≈ 0.3". Without this, H2-H3
separability is conditional on an unverified premise.

---

## Prat-Carrabin on L05 — Theoretical coherence

The README anchors H3 on Wei-Stocker 2015 and H4 on Prat-Carrabin-Gershman
2024/2025, citing both. These are not merely complementary accounts;
they make **mutually exclusive attributions** for where SD(θ) inflation
comes from. WS2015 says it comes from gain modulation of encoding
precision by the prior. PCG2025 says it comes from prior skewness acting
through a constant-precision code. The data can decide between them,
but only if the simulator's framing separates them.

Currently it does not. H3's signature ($\alpha_{\mathrm{sda}} \approx
1 + \eta$) is derived on the *parametric assumption* that
$\sigma_e = \sigma_0 / p^{\eta}$; under that assumption, my mechanism
(prior-only anti-Weber with $\sigma_e = \sigma_0$) gives a different
SD curve, but only because the simulator has chosen to attribute the
tail inflation to $\eta > 0$. An identifiability test between the two
mechanisms must vary a quantity that dissociates them —
**specifically, the shape of $\sigma_e(\theta)$ at fixed
$p(\theta)$**. The simulator's H2 / H3 / H5 contrast varies $\eta$
while $p(\theta)$ is held at the experimental prior; this is
confounded with the prior-only mechanism.

Hahn & Wei's 2022 additive-decomposition paper is already the correct
unifying lens: bias has two components — prior attraction and
likelihood repulsion — whose relative weight is a single ratio. The
simulator should parameterise the five cells as points on this one
ratio and admit that H3 vs. my account is not a discrete cell
comparison but a 1-parameter continuous contrast. Framing them as
discrete cells is category-theater; the underlying family is
continuous.

**Demand**: re-express H2 / H3 / H5 as a single parametric observer
with $\mathcal{J} \propto p^{\alpha}$, $\alpha$ free — Prat-Carrabin
& Woodford 2020 already does this for numerosity. The five-cell
matrix becomes three cells (linear-Weber, log-encoding-family,
efficient-family) with continuous $\alpha$-axis in the last two.

---

## Ganguli on L06 — H6 / H7 candidate assessment

H6 (power-law encoding $f(\theta) = k \cdot \theta^{q}$, constant noise)
and H7 (prior-only anti-Weber observer) were flagged in R1 L01 as
candidate additions. From a population-coding standpoint, they are not
*new* cells — they are endpoints of the $\alpha$-axis Prat-Carrabin
just argued for.

Power-law encoding with exponent $q$ and constant sensory noise gives
Fisher information $\mathcal{J}(\theta) = q^{2} \cdot \theta^{2(q-1)} /
\sigma_0^{2}$. This is a function of $\theta$ alone (prior-independent),
and its *relationship to the prior* is whatever the population
structure imposes. When the prior is
$p(\theta) \propto \theta^{-\beta}$ (power-law with exponent $\beta$),
mutual-information maximisation links $q$ and $\beta$ by
$\mathcal{J} \propto p^{\alpha}$ with $\alpha = 2(q-1)/(-\beta)$. The
H6 proposal therefore slots into the $\alpha$-axis at a specific
$(q, \beta)$ pair — it is not a distinct theoretical object from H2 /
H3 if we accept the Prat-Carrabin reframing.

H7 is the other endpoint: $\alpha = 0$ (constant encoding precision),
with all SD variation coming from prior-skew alone. This is the PCG 2025
mechanism and is the natural **null hypothesis** for the efficient-
coding family. Dropping H7 because "its prediction lies on the convex
hull" is exactly wrong — the null is supposed to live on the convex
hull. Not having an explicit $\alpha = 0$ cell means the efficient-
coding family has no reject-to-null option.

Cicchini, Anobile, Burr (2014) empirically recovered $q \approx 0.5$
(square-root) for numerosity, not Weber ($q = 0$ on a log scale). The
simulator's current family places *no* point at $q = 0.5$; both H1
and H4 approximate Weber. This is a genuine gap.

**Recommendation**: do not add H6 and H7 as discrete cells. Instead,
replace the five-cell matrix with a two-axis parameterisation
— encoding-family × efficient-coding-strength $\alpha$ — and report
predictions on a continuous grid. Keep H1 and H4 as named subtypes
of the linear / log axis for anchor-paper traceability, but retire
the claim that H2, H3, H5 are discrete testable hypotheses.
