# R1 External-research findings

**Date**: 2026-04-18.
**Tools used**: Zotero MCP (semantic_search × 3), WebSearch × 3. K-Dense Web
deep-research queue is recommended but must be launched manually by the
user at [www.k-dense.ai](https://www.k-dense.ai) — K-Dense delivers
longer-form synthesis the in-session tools cannot.

**Lenses served**: L04 design-prediction circularity, L05 theoretical
coherence across the 8 refs, L06 H6/H7 candidate assessment.

---

## 1. Papers newly surfaced (not in the 8-anchor list)

### Directly germane to L04 (prior-learning fidelity)

- **Luu, Stocker & Donner (2018)** — *Post-decision biases reveal a
  self-consistency principle in perceptual inference.* Key finding:
  "all subjects seemed to substantially overestimate the width of the
  stimulus prior as compared to the true stimulus distribution." Under
  mirror-skew α=±3.3 priors, a subject who internalises a broader
  subjective prior will flatten the BOEC repulsion signature — the
  simulator's veridical-prior assumption may *underestimate* the real
  width.
- **Roach, McGraw, Whitaker, Heron (2016)** — *Generalization of prior
  information for rapid Bayesian time estimation.* "The limited
  opportunity afforded by each of our brief testing blocks resulted in
  partial prior recalibration — note how indifference points fall close
  to the midpoint between the mean of the relevant duration
  distribution and that of the entire stimulus set." Directly
  undermines the assumption that subjects fully learn the
  mirror-skew prior in a realistic session.
- **Acerbi, Wolpert & Vijayakumar (2012)** (re-read §7): "All recovered
  priors are (on average) heavy tailed … the subjects' internal
  representations are actually heavy-tailed." Even when the
  experimental prior is compact, the inferred subjective prior is
  heavier-tailed — again, softening the BOEC tail inflation.
- **Wiener et al. (2014)** — *Continuous Carryover of Temporal Context
  Dissociates Response Bias from Perceptual Influence for Duration.*
  Carry-over effects persist even after the prior is learned;
  trial-history adaptation competes with the stationary-prior
  assumption the simulator makes.
- **Charlton et al. (2023)** — *Environmental dynamics shape
  perceptual decision bias.* Argues that subjects use a *dynamically
  evolving* prior; the effective prior at trial t is not what the
  experimenter imposed.

### Directly germane to L05 (theoretical coherence across refs)

- **Hahn & Wei (2024/journal-version of 2022 preprint)** — confirms the
  additive-decomposition framework is the unifying lens that subsumes
  BOEC (Wei-Stocker 2015) and prior-attraction (Stocker-Simoncelli
  2006) as *two components of a single Bayesian observer*. Critical
  quote: "the bias of the Bayesian mean comprises two components: one
  driven by the prior, and one driven by the precision of the
  encoding. If the encoding is 'efficient', the two components have
  opposite effects; their relative strengths are determined by the
  objective that the encoding optimizes."
- **Fritsche, Spaak & De Lange (2020)** — *A Bayesian and efficient
  observer model explains concurrent attractive and repulsive history
  biases in visual perception* (eLife). Key extension: "we allowed
  predictions used for optimising encoding and decoding to be based on
  potentially distinct transition distributions and integration time
  constants." I.e., the *encoding prior* can differ from the
  *decoding prior*. The simulator forces these to be the same
  (veridical); this is a modelling choice, not a theoretical
  constraint.
- **Petzschner, Glasauer & Stephan (2015)** — *A Bayesian perspective
  on magnitude estimation* (TICS review). Argues: "Scalar variability
  is equally well explained by a linear increase in noise with
  increasing magnitudes on linear scales or by a logarithmic
  representation of magnitude with fixed variability [Weber-Fechner
  equivalence]." Integrates Stevens' power law + Weber-Fechner via
  Bayesian framework. Relevant to whether H1 and H4 are
  indistinguishable in principle (they are), and whether H6 (power-law
  encoding) would add genuinely new predictions (it would, via the
  exponent).
- **Zhang & Stocker (2021)** — *Prior Expectations in Visual Speed
  Perception Predict Encoding Characteristics of Neurons in Area MT.*
  Neural validation: MT tuning curves are log-like and tile stimulus
  space with near-uniform density — supports efficient-CDF encoding
  at the population level. Narrows one escape-hatch for dismissing
  H2/H3 as "purely behavioural constructs".
- **Petzschner, Glasauer, Stephan (2015 J. Neurosci, different paper
  from above)** — *Iterative Bayesian Estimation as an Explanation
  for Range and Regression Effects.* Provides the direct link between
  Weber-Fechner, Stevens' power law, and Bayesian fusion via
  log-scale coding + response-mapping. Suggests a **Stevens-exponent
  observable** — the response-mapping slope in log-log — that is
  orthogonal to the simulator's two primary discriminators.

### Directly germane to L06 (H6 / H7 candidates)

- **Prat-Carrabin & Woodford (2020)** — *Efficient coding of numbers
  explains decision bias and noise.* Exactly the H6 proposal:
  "variable precision of encoding is specified by a Fisher information
  function that is efficiently chosen with regard to a subjective
  prior, and the decoded value of each number is the Bayesian-mean
  estimate based on the encoded evidence." Crucially parameterises
  the Fisher information as $\mathcal{J} \propto p^{\alpha}$ with
  $\alpha$ free — subsumes H2 ($\alpha = 2$ after back-transform), H3
  with $\eta$, and a continuous family of "strength-of-efficient-
  coding" cells. The BOEC family could be re-expressed as a single
  H with $\alpha$ parameter, simplifying the hypothesis space.
- **Cicchini, Anobile & Burr (2014)** — *Compressive mapping of
  number to space reflects dynamic encoding mechanisms, not static
  logarithmic transform.* Challenges Weber's law as universal: "for
  discrimination of numerosity Weber's law applied over only a very
  limited interval, with the square-root law (α = 0.5) operating over
  most of the range." Implies a power-law encoding with exponent 0.5
  is empirically preferred over Weber in at least one magnitude task
  — a concrete anchor for H6.
- **Prat-Carrabin & Gershman (2025** — note year correction from our
  earlier entry; the journal version is 2025**)** — *Bayesian
  estimation yields anti-Weber variability.* Re-read: key quote —
  "many encoding schemes yield Weber's law, provided that their
  Fisher information is inversely related to the square of the
  magnitude. … This account of Weber behaviors with a linear encoding
  does not however preclude the possibility of a logarithmic,
  Fechnerian encoding … we find that the most prevalent model
  features such a logarithmic encoding." Direct support for a unified
  $\mathcal{J} \propto 1/\theta^{2}$ family that the simulator's H1
  and H4 both satisfy but do not currently parameterise.

### Supplementary / context

- **Sohn & Lee (2013)**, **Narain et al. (2018)**, **Natsume et al.
  (2025)** on prior learning dynamics in timing — relevant to L13
  (prior-learning dynamics, not this round).
- **Nieder (2016)** — logarithmic neural coding of number; confirms
  Fechner's hypothesis at neural level for numerosity.
- **Laquitaine & Gardner (2018)** — *A Switching Observer* — subjects
  switch between prior- and likelihood-based estimation over session;
  observer models that assume constant strategy are misspecified.
- **Jegminat et al. (2019)** — *Bayesian regression explains how human
  participants handle parameter uncertainty* — bimodal response
  distributions from switching, argues against naive BLS.
- **Thakur et al. (2021)** — implicit vs. explicit prior learning;
  different dynamics and different asymptotic biases.

---

## 2. Integrated findings by lens

### L04 — Design-prediction circularity

The mirror-skew parameter α=±3.3 was inherited from the p1_make_base_config
defaults; no published paper independently endorses this value for timing
tasks. Three literatures converge to suggest the *effective* subjective
prior in a short session differs from the imposed one:

1. Subjects overestimate prior width (Luu et al. 2018) — effective |α|
   smaller than 3.3.
2. Subjects partially recalibrate in brief blocks (Roach et al. 2016) —
   indifference points move toward the global mean, not the block mean.
3. Subjects build heavy-tailed internal priors (Acerbi 2012) — even with
   a compact experimental prior.

Each effect damps the BOEC repulsion signature and softens the contrast
with the classical attractive family. The design-prediction circularity
concern (R1 R1 L01) is therefore attenuated by these subject-side
deviations — the simulator would see smaller BOEC-vs-classical
separations in real data than its veridical-prior predictions suggest.

### L05 — Theoretical coherence

Hahn-Wei 2022 already provides the unifying lens. Fritsche et al. 2020
demonstrates that encoding-prior and decoding-prior can formally differ,
expanding the cells a unified framework must cover. Petzschner 2015
TICS review ties Weber-Fechner and Stevens' power law together via
Bayesian fusion on a log-scale. The existing simulator is not
internally incoherent, but it is **over-discrete**: H2/H3/H5 are three
points on a continuous $\eta$-axis rather than three separate cells,
and H1/H4 are indistinguishable endpoints of an encoding-continuity
family.

### L06 — H6 / H7 candidates

- **H6 (power-law encoding, f ∝ θ^q)** is *not* a new proposal — it is
  the Prat-Carrabin & Woodford 2020 model, which has a direct
  empirical anchor (Cicchini et al. 2014 finds q ≈ 0.5 for numerosity).
  Adding H6 as a parametric *axis* (rather than a discrete cell)
  would honour both the theoretical unification of H2-H3-H5 (Hahn-Wei
  2022 decomposition) and the empirical cases that do not collapse to
  Weber.
- **H7 (linear encoding + constant noise + skewed subjective prior,
  isolating the prior-only anti-Weber mechanism)** is effectively
  realised already by PCG 2025 in numerosity. The simulator needs H7
  *only if* the mirror-skew design is shown (via L04 analysis) to
  preserve enough prior-shape fidelity; otherwise H7's signature is
  washed out by the subject-side deviations above and adding the cell
  is expensive for little benefit.

**Roadmap implication**: the next simulator-side amendment should be
a parametric re-framing of the BOEC family (H2-H3-H5 → single observer
with $\mathcal{J} \propto p^{\alpha}$, $\alpha$ free), not more
discrete cells.

---

## 3. K-Dense Web prompt (for user-invoked deep research)

The following prompt is staged for a K-Dense Web deep-research session
the user can launch at [www.k-dense.ai](https://www.k-dense.ai); the
in-session tools do not cover this depth of cross-disciplinary
synthesis.

> Synthesise the relationship between (a) efficient-coding Bayesian
> observer models (Wei-Stocker 2015, Hahn-Wei 2022, Hahn-Wang-Wei
> 2025), (b) power-law / Stevens-exponent models of magnitude
> perception (Prat-Carrabin & Woodford 2020, Cicchini et al. 2014),
> and (c) prior-learning dynamics in timing (Acerbi 2012, Sohn-Lee
> 2013, Narain et al. 2018, Roach et al. 2016). Specifically: for
> mirror-skew prior designs in interval timing, what is the smallest
> sufficient parametric observer family that subsumes (a)-(c)?
> Report the family, the number of free parameters, and the
> identifiability conditions on multi-noise-level or
> multi-prior-shape data.
