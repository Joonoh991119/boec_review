# R7 External-research findings

**Date**: 2026-04-18.
**Lenses**: L19 Bayesian Efficient Coding & likelihood-shape (PPC)
frameworks · L21 competing unified accounts (dynamical / resource-
rational).
**Tools**: Zotero MCP × 2 + WebSearch × 2.

---

## L19 — Meta-framework alternatives to Wei-Stocker efficient coding

The simulator commits to Wei-Stocker 2015 efficient coding: encoding
maximises $I(m; \theta)$ under a power constraint, with Gaussian
additive noise. This is one choice of meta-framework. Two
alternatives are standard in the literature but absent from the
simulator:

### Bayesian Efficient Coding (Park & Pillow 2024)
Reference: **Park, I. M. & Pillow, J. W. (2024).** *Bayesian
Efficient Coding.* bioRxiv preprint. DOI:
10.1101/178418.

Key claim: efficient coding should be defined relative to a
*Bayesian loss function* rather than mutual information.
Different losses → different optimal encodings. Direct quote:
"A Bayesian efficient code is one for which parameters $\theta$ are
set to minimize the average loss over stimuli and responses drawn
from the prior and encoding model, subject to the resource
constraint on the encoder, $C(\theta) < c$."

- MI-maximising codes (Wei-Stocker tradition) may be **inefficient**
  with respect to loss functions that care about posterior *shape*
  rather than entropy.
- BEC therefore adds a new axis to the hypothesis space: the
  **encoding loss** (squared-error? absolute? log-score?) — distinct
  from the decoder's loss that the simulator's §Design axes already
  closes to $L^{2}$.
- Concrete example: for posterior-variance minimisation as the
  encoding loss, the optimal code differs from the MI-maximising
  CDF encoding. This means H2/H3/H5 are optimal *only* under the
  Wei-Stocker MI objective; under a BEC observer with
  posterior-variance-minimising encoding, the α-axis does not
  index all cells.

### Probabilistic Population Codes (Ma-Beck-Latham-Pouget 2006 tradition)
References: **Ma et al. 2006 (Nat. Neurosci.)**, Beck-Latham-Pouget
(2011, J. Neurosci.), Pouget-Beck-Ma-Latham (2013, Nat.
Neurosci.), Walker-Cotton-Ma-Tolias (2020, Nat. Neurosci.).

Key claim: uncertainty is encoded in the *shape* of the population
activity distribution, not just a scalar. Poisson-like variability
gives Gaussian-in-stimulus-space likelihoods under linear tuning
assumptions; divisive normalisation (Beck-Latham-Pouget 2011) gives
rise to non-Gaussian likelihoods.

- PPC is a *structural* meta-framework: it constrains how
  probability distributions are encoded at the neural level.
- The simulator's m-space formulation collapses this population
  representation to a scalar $m$, absorbing all PPC shape
  information into the Gaussian-noise assumption in Bundle B item
  (i).
- Walker-Cotton-Ma-Tolias (2020) V1 data provides direct neural
  evidence for PPC; Wei-Stocker and Zhang-Stocker MT data provide
  direct neural evidence for efficient-CDF. These are two different
  neural theories of the same behavioural phenomenon.

### Polanía-Woodford-Ruff (2019) efficient coding of *value*
Extends efficient coding to subjective-value representation, not
stimulus representation. Orthogonal to the simulator but a
reminder that "efficient coding" can be applied to any
computationally-relevant variable.

**Refs outside 8-anchor (L19)**: Park-Pillow 2024, Ma-Beck-Latham-
Pouget 2006, Beck-Latham-Pouget 2011, Pouget-Beck-Ma-Latham 2013,
Walker-Cotton-Ma-Tolias 2020, Polanía-Woodford-Ruff 2019. **6
widening citations.**

---

## L21 — Competing unified accounts (dynamical and resource-rational)

### Dynamical recurrent-network efficient coding
Reference: **Prat-Carrabin, A., Harl, M. V. & Gershman, S. J. (2026,
bioRxiv preprint).** *Fast efficient coding and sensory adaptation
in gain-adaptive recurrent networks.* DOI: 10.1101/2025.07.11.664261.

Key claim: efficient coding emerges from *network dynamics* rather
than static tuning. Gain-adaptive recurrent networks produce
"fast adaptive tuning curves" that minimise a spiking-cost-weighted
loss. Critical findings:

- **For wide priors**: optimal gain configuration yields prior
  **attraction**.
- **For narrowly-peaked priors**: optimal gain configuration places
  maximal gains *at some distance from the peak*, yielding **adapter
  repulsion**.
- The simulator's mirror-skew design ($\omega \approx 0.34$) is
  neither wide-uniform nor narrowly-peaked: predictions from
  PCHG2026 would combine attraction and repulsion contributions in
  an adaptation-history-dependent way.

Implication: the simulator's **static-tuning-curve assumption**
(unstated but implicit) is an additional meta-framework
commitment. Under PCHG2026, the predicted $(b_A, b_R)$ sign
pattern depends on how recent trials have adapted the gain.

Related dynamical-recurrent-network work:
- **Gonzalo Cogno et al. (2023, arXiv).** Adaptive coding
  efficiency in recurrent cortical circuits via gain control.
- **Barrett et al. (2021, PLOS Comput. Biol.).** Efficient and
  robust coding in heterogeneous recurrent networks.
- **Ali et al. (2023, PNAS).** Predictive coding as a consequence
  of energy efficiency in recurrent neural networks.

### Resource-rational analysis
References: **Lieder & Griffiths (2020, Behavioral and Brain
Sciences).** *Resource-rational analysis.* **Bhui, Lai & Gershman
(2021).** *Resource-rational decision making.* **Icard (2024).**
*Resource Rationality: Toward a Theory of Cognitive Economy.*

Key claim: the observer uses *bounded* computational resources;
optimal decisions are the best achievable given the resource
budget. Bayesian observers are a special case (unlimited
computation). Resource-rational accounts predict systematic
*deviations* from optimal Bayesian inference that depend on
task difficulty and available computation time.

- In the mirror-skew design, resource-rationality predicts biases
  that depend on ITI, on cognitive load from preceding trials, on
  response deadlines — variables the simulator does not vary.
- Bhui-Lai-Gershman 2021 integrates RR with sequential-sampling
  models (TDDM from R3 L12 is a special case).

### Rational inattention
Reference: **Woodford (2020).** Rational inattention in economics;
applied to perceptual tasks by Prat-Carrabin-Woodford (2020, R2 L07
introduction). Observer allocates limited attention to minimise
expected loss; precision grows with stakes.

Gershman et al. (2020-2024) connect rational inattention to tonic
dopamine and reward.

**Refs outside 8-anchor (L21)**: Prat-Carrabin-Harl-Gershman 2026,
Gonzalo Cogno et al. 2023, Barrett et al. 2021, Ali et al. 2023,
Lieder-Griffiths 2020, Bhui-Lai-Gershman 2021, Icard 2024,
Mandelbaum et al. (BBS commentary), Woodford 2020,
Prat-Carrabin-Woodford 2020. **10 widening citations.**

---

## Integrated finding: the simulator's meta-framework commitment

The simulator has so far named its parametric commitments
(§Parametric commitments, R6) and its auxiliary assumptions
(§Bundle B, R4+R5). It has NOT named its **meta-framework
commitment** — which is Wei-Stocker static-MI efficient coding.
This is a distinct layer of commitment. R7 requires an amendment
that adds a **§Meta-framework commitment** block stating:

- The simulator commits to Wei-Stocker-style static-tuning
  efficient coding with MI-maximising objective.
- Alternative meta-frameworks (BEC, PPC, gain-adaptive recurrent,
  resource-rational, rational inattention) are NOT within scope.
- HMC conclusions are conditional on the meta-framework choice,
  not just on Bundle B auxiliaries.
- The α-axis (R1) indexes hypotheses within the WS meta-framework;
  it does not index BEC, PPC, or dynamical-recurrent observers.

## Aggregate widening

16 refs outside the 8-anchor set. Cumulative R1-R7: ≈ 100 refs.

## K-Dense Web prompt (user-launched)

> Compare the predictions of (a) Wei-Stocker 2015 static efficient-
> CDF coding, (b) Park-Pillow 2024 Bayesian Efficient Coding with
> variance-minimising encoding loss, (c) Prat-Carrabin-Harl-Gershman
> 2026 gain-adaptive recurrent networks, and (d) Ma et al. 2006
> probabilistic population codes with divisive normalisation for a
> mirror-skew duration-reproduction experiment (α = ±3.3, ω = 0.34,
> 700 trials × 30 subjects). Report the (bias, SD) signature each
> framework predicts at θ = 1.1 s. Identify meta-framework-
> disambiguating observables.
