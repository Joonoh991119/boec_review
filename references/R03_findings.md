# R3 External-research findings

**Date**: 2026-04-18.
**Lenses**: L11 (empirical precedent for efficient-CDF in timing),
L12 (alternative observer frameworks), L13 (prior-learning dynamics).
**Tools**: Zotero MCP × 3 + WebSearch × 3.
**Widening discipline**: each section ends with "refs outside the 8-anchor set" count.

---

## L11 — Empirical precedent for efficient-CDF encoding in interval timing

Wei-Stocker 2015 (anchor) proved the CDF-encoding framework using
ORIENTATION data (Girshick et al. 2011 natural-scene prior). Zhang &
Stocker 2021 extended to speed perception using MT physiology
(Nover et al. 2005; Burge & Geisler 2015). **The interval-timing
literature has no corresponding demonstration.**

### Positive evidence for logarithmic encoding in timing
- **Nieder (2016)** — "The neuronal code for number" — numerosity
  neurons tile log-scale with near-symmetric tuning; consistent with
  Fechner-log but NOT CDF per se.
- **Logarithmic encoding of ensemble time intervals (Roach et al.
  Sci Rep)** — timing intervals coded logarithmically, but via
  *oscillatory / beat-frequency* mechanisms (striatal beat-frequency
  model, Matell-Meck 2004) rather than Fisher-information
  allocation by prior density.

### Population-clock evidence against uniform-density encoding
- **Paton & Buonomano (2018, Neuron)** — *The Neural Basis of Timing:
  Distributed Mechanisms for Diverse Functions.* Time is encoded by
  **population clocks**: dynamically changing activity patterns
  (ramping cells, sequential firing) rather than by a static,
  prior-density-proportional allocation of tuning curves. The
  Wei-Stocker efficient-coding framework assumes a static code with
  tuning-curve density $\propto \sqrt{p(\theta)}$; population clocks
  are fundamentally dynamic and do not satisfy this density rule.
- **Mello, Soares & Paton (2015)** — *A Scalable Population Code for
  Time in the Striatum.* Individual striatal neurons fire at different
  times within the interval; trial-to-trial variation in duration
  judgements is predicted by population dynamics, not by any
  Fisher-information structure imposed by the prior distribution.
- **Narain et al. (2018, Nature Communications)** — cerebellar
  mechanism for learning prior distributions; proposes a specific
  neural circuit for PRIOR learning, but the encoding itself remains
  ramp / basis-set — not efficient-CDF.

### Consequence for the simulator
The efficient-CDF encoding that defines H2, H3, H5 is a **faith-based
port** from orientation/speed to duration. No interval-timing neural
study reports MT-style log-tiling tuning curves distributed according
to the prior's CDF. If the neural code for duration is a population
clock (ramping or sequential), the very concept of $f(\theta) =
k \cdot F_{\mathrm{prior}}(\theta)$ is inapplicable in this domain;
the simulator's cells are then theoretical abstractions without
neural-level support.

**Refs outside 8-anchor set**: Paton-Buonomano 2018, Mello-Soares-Paton
2015, Nieder 2016, Matell-Meck 2004 (via Paton-Buonomano), Roach et
al. Sci Rep, Wittmann 2009, Ivry-Spencer 2004 (via Wittmann). **7
widening citations.**

---

## L12 — Alternative observer frameworks

The simulator's 5-cell matrix is entirely inside the
efficient-coding-Bayesian-observer family. Three alternative families
are standard in the interval-timing literature and have **no cell**
in the simulator:

### Adaptive drift-diffusion models
- **Simen et al. (2013, *J. Neurosci.*)** — *An adaptive drift-
  diffusion model of interval timing dynamics.* Time-adaptive DDM
  (TDDM) with real-time adaptation; preserves scalar invariance
  without a Bayesian posterior.
- **Rivest & Bengio (2011)** — DDM applied to peak-interval
  procedure.
- **Simen, Rivest et al. (2011, *PLoS Comput. Biol.*)** — extension
  to interval discrimination.
- For duration REPRODUCTION, TDDM and BLS Bayesian observer make
  similar first-order predictions (mean bias, scalar SD) but
  differ in (i) response-time distribution, (ii) trial-by-trial
  dynamics, (iii) adaptation timescale. None of these predictions
  is currently in the simulator.

### Population-clock / oscillator frameworks
- **Paton & Buonomano 2018** (above) — ramping and sequential codes
  give scalar variability without any Bayesian inference.
- **Matell & Meck (2004)** — striatal beat-frequency model.
- **Buhusi & Meck (2005)** — review of interval-timing mechanisms.
- Predictions are qualitatively different: population-clock models
  predict response SD that depends on **accumulated noise in the
  network dynamics**, not on Fisher information of any encoding.

### Reinforcement-learning / resource-rational accounts
- **Bhui, Lai & Gershman (2021)** — *Resource-rational decision
  making* — unifies sequential-sampling with bounded-optimality.
- **Gershman (2021)** — reward-based prior updating; predicts
  distortion of the subjective prior by utility gradients.
- **Woodford (2020)** — rational inattention; observer allocates
  attention/precision to minimize expected-loss-weighted prediction
  error. Equivalent to Hahn-Wei 2022 **only if** the loss is
  squared error; deviates otherwise.

### Consequence
The simulator's "5-cell matrix" is Bayesian monoculture. Non-Bayesian
alternatives (TDDM, population clock) can produce the same first-
order behavioural signatures (attractive S-shape bias, scalar SD)
*without* any prior-encoding machinery. The simulator's HMC
conclusions will therefore be *conditional on the Bayesian
framework being the correct meta-model*. This conditional should be
stated explicitly.

**Refs outside 8-anchor set**: Simen et al. 2013, Rivest-Bengio
2011, Simen-Rivest 2011, Paton-Buonomano 2018 (repeat),
Matell-Meck 2004, Buhusi-Meck 2005, Bhui-Lai-Gershman 2021,
Gershman 2021, Woodford 2020. **9 widening citations.**

---

## L13 — Prior-learning dynamics

The simulator assumes a stationary subjective prior. Four
empirical findings contradict this in the exact regime the mirror-
skew duration experiment occupies:

### Prior width shrinks across sessions
- **Sohn & Lee (2013, *J. Neurophysiol.*)** — fit a three-parameter
  Bayesian observer across 10 sessions; "the width of the prior,
  not the likelihoods, gradually shrinks over sessions." The
  subjective prior at session 1 has markedly larger variance than
  at session 10.

### Asymmetric learning rates for wide→narrow vs. narrow→wide
- **Narain et al. (2018)** — "participants' adjustments were slower
  when the prior switched from a wide to narrow distribution of
  intervals compared to vice versa." This is a prior-shape-
  asymmetric learning law; mirror-skew is one symmetry, but the
  learning *rate* to it depends on the direction of the switch.

### Prior learning on brief-block timescale
- **Roach, McGraw, Whitaker & Heron (2016, PNAS)** — prior learning
  occurs within a single brief block; indifference points
  partially recalibrate within tens of trials. But "partial prior
  recalibration" is the phrase: subjects do NOT fully learn the
  block-specific prior.
- **Wang, Luo, Ivry, Tsay, Pöppel, Bao (2023, PLoS Comput Biol)** —
  *A unitary mechanism underlies adaptation to both local and global
  environmental statistics in time perception.* Single adaptive
  mechanism integrating over multiple timescales — not the
  stationary posterior the simulator assumes.

### Carryover and serial dependencies
- **Wiener, Thompson, Coslett & Meck (2014)** — continuous carryover
  of temporal context dissociates response bias from perceptual
  influence. Trial $t$'s response depends on trials $t-1, t-2,
  \ldots$
- **Cheng, Chen & Shi (2024)** — *Opposing sequential biases in
  direction and time reproduction.* Attractive in time, repulsive
  in direction; task-relevance and WM modulate the effect.
- **Bévalot & Meyniel (2023, *Nat. Commun.*)** — implicit vs.
  explicit prior learning produce different dynamics; priors are
  learnt at different timescales for different representational
  formats.

### Consequence
The simulator's HMC will fit a single static prior to data from a
session during which the effective prior demonstrably evolves. The
fitted prior will be a *time-average* of the dynamic prior, not
the prior the subject was using at any given trial. For BLS with
time-averaged prior, bias predictions can be close to correct; for
$\alpha_{\mathrm{sda}}$, the time-averaging introduces an
independent source of SD inflation that must be separated from
encoding-driven SD inflation.

**Refs outside 8-anchor set**: Sohn-Lee 2013 (repeat), Narain
2018 (repeat), Roach 2016, Wang-Luo-Ivry 2023, Wiener 2014,
Cheng-Chen-Shi 2024, Bévalot-Meyniel 2023, Flesch-Saxe-Summerfield
2023, Gekas et al. (via Hahn-Wei 2024), Kerrigan-Adams (via Roach).
**10 widening citations.**

---

## Aggregate widening count for R3

**26 refs outside the 8-anchor set cited.** Far above the minimum of
5 per round.

## K-Dense Web prompt for user

> Locate interval-timing neural recording studies that could be
> interpreted as evidence for (or against) Wei-Stocker 2015 efficient-
> CDF encoding in time. Specifically: does any timing paper find MT-
> style log-tiling with neuron density proportional to sqrt(prior)?
> If not, what is the closest neural match, and what does that imply
> for porting H2/H3/H5 to duration data?
