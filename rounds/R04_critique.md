# R4 Critique — three personas

**Lenses**: L08 experimental-parameter sensitivity (Popper) · L10
generative-model assumption audit (Quine, Fool).

---

## Popper on L08 — parameter commitments are unreported

The mirror-skew prior α = ±3.3, ω = 0.3374 is presented as "the
experimental prior." It is not. It is one point in a
multi-dimensional parameter space the experimenter chose. Every
rejection threshold and discriminator band in the simulator holds
*conditional on these specific parameter values being the ones the
actual experiment uses*. If α turns out to be ±2.5 or ω = 0.25,
all bands tighten or loosen accordingly, and the honest falsifier
must be stated as a *band over parameter space*, not a point.

The literature already contains the tools. Depaoli, Winter & Visser
(2020, Frontiers in Psychology) provide the sensitivity-analysis
method: fit the posterior under a lattice of prior hyperparameters
and report the *band of posteriors*. Sridharan & Castiglione (2014,
Int. J. Approx. Reasoning) do this specifically for skew-normal
class priors. Manning et al. (2022, eNeuro) show this for Bayesian
observer models directly.

Two demands:

1. State the mirror-skew parameter choice as a commitment, not a
   fact. "This simulator runs on (α = 3.3, ω = 0.3374)." Then
   report the robustness band: for α ∈ [±1.5, ±5.0] and ω ∈ [0.15,
   0.40], is the R1-R3 discriminator framework still falsifiable?
2. **Log-uniform stimulus spacing**: the simulator uses a linear θ
   grid. Log-uniform spacing would break the H1↔H4 degeneracy that
   R1 flagged as unresolvable. Adding log-uniform spacing as an
   alternative design condition is a concrete design amendment the
   simulator could advocate, on falsifiability grounds — without
   it, H1 vs. H4 is permanently indeterminate.

A rejection threshold that holds on a single point of parameter
space and dissolves on a lattice is not really a rejection threshold.
It is a decoration around a pre-committed point estimate.

---

## Quine on L10 — auxiliary assumptions are a bundle

The simulator's generative model carries **seven** auxiliary
assumptions, each of which is declared in passing rather than
audited:

1. Gaussian encoding noise in m-space (→ required for efficient-
   coding MI bound per Wei-Stocker 2016).
2. Veridical subjective prior (R1 + R3 caveats applied).
3. Stationary prior (R3 caveat applied).
4. No motor noise at the behavioural level (HWW 2025 §2.5 proves
   this is safe for identifiability; but reality has motor noise).
5. No lapse rate (Acerbi-Vijayakumar-Wolpert 2014 standard include;
   simulator omits).
6. L² / BLS readout (R2 caveat applied).
7. Additive $\delta$ on $f(\theta)$ rather than multiplicative on
   $\theta$ (approximation for small-noise regime; Harris-Wolpert
   1998 shows multiplicative is also plausible).

When the simulator reports the $\alpha$-posterior from HMC, the
posterior reflects data conditional on ALL SEVEN auxiliaries
holding simultaneously. The bundle declaration from R2 L14 (Quine
on Q(θ)) must be extended to the α-posterior itself: "Q(θ) and
α-posterior both assume Bundle B." The caveats currently written in
separate sections of the README; they should be consolidated into a
single Bundle declaration near the Discriminating-observables
table.

This is not a demand for rejection. The bundle is large but each
element has literature support. The demand is for **honesty about
the bundle size**. When a reader sees "α-posterior favours H3 over
H2", they should see alongside it the full Bundle B they are
implicitly accepting.

---

## Fool on L10 — why even Gaussian noise?

Every paper in the Wei-Stocker tradition assumes Gaussian effective
noise. Wei-Stocker 2016 proves it is *necessary* for the tight
MI bound. But from a pure-mechanism standpoint — the brain is a
Poisson-spiking machine. Why should the behavioural noise be
Gaussian at all?

Keemink et al. 2018 and Park-Pillow 2024 show it approximately is,
at the level of bias curves, due to decoding across a population.
Prat-Carrabin-Harl-Gershman 2026 show recurrent networks produce
Gaussian effective noise from Poisson spike trains. Good — so
Gaussian IS mechanistically defensible.

But the simulator does not cite any of this. The Gaussian
assumption sits on top of a Wei-Stocker 2016 proof that depends
on the Gaussian in the first place. This is technically consistent
but theoretically incestuous: the efficient-coding framework makes
the Gaussian assumption because it simplifies the MI bound, and
then claims the Gaussian framework explains behavioural data
without separately justifying why behaviour should be Gaussian-
distributed. The population-code literature IS the separate
justification; but the simulator does not know it yet.

Two demands:

1. Cite Keemink 2018 / Park-Pillow 2024 / Prat-Carrabin-Harl-
   Gershman 2026 as the *behavioural-level* justification for
   Gaussian noise. This removes the incestuous loop.
2. Admit that if the behavioural noise is measurably non-Gaussian
   (e.g. Gamma-distributed RT, skewed response distributions), the
   $D_0$ correction (already in the simulator via R5) is the
   first-order fix but is insufficient for large deviations.
   Commit a band: if response-distribution skewness |γ| > 0.5, the
   efficient-coding framework's MI tightness is violated and all
   α-posteriors above/below a threshold are not trustworthy.

The devil's advocacy is not that Gaussian is wrong — it is that the
simulator silently assumes it without showing the work. Show the
work.
