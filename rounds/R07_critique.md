# R7 Critique — three personas

**Lenses**: L19 BEC & PPC (Ganguli) · L21 dynamical and resource-
rational alternatives (Fool + Hahn).

---

## Ganguli on L19 — the α-axis does not subsume BEC or PPC

The R1 synthesis asserted that H2/H3/H5 are three sampled points on
a continuous $\alpha$-axis. That is correct *within* the
Wei-Stocker meta-framework. It is NOT a universal axis.

Park & Pillow 2024 (Bayesian Efficient Coding) show that the
optimal encoding depends on what loss function you are optimising
*during encoding*. MI-maximisation (Wei-Stocker) is ONE loss;
posterior-variance-minimisation, log-score-maximisation, and
weighted-squared-error all give different optimal codes. The
α-axis parameterises the noise scaling under MI, but under a BEC
observer with posterior-variance-minimising encoding, the optimal
tuning curves are not simple CDFs.

PPC (Ma-Beck-Latham-Pouget 2006 and descendants) introduces a
completely different dimension: likelihood *shape*. The simulator
collapses this to a scalar via its m-space formulation and
Gaussian-noise assumption (Bundle B item i). If the neural code is
a PPC with divisive normalisation (Beck-Latham-Pouget 2011), the
likelihood has non-Gaussian shape that the simulator's D_0
correction (R5 reference) handles only to first order.

Demand: the simulator should add a **§Meta-framework commitment**
block stating that it commits to Wei-Stocker static-MI efficient
coding; that BEC and PPC are distinct meta-frameworks not covered
by the α-axis; and that any finding "favouring" BOEC in the HMC
must be read as "favouring BOEC *within* the Wei-Stocker meta-
framework."

Without this, a reader who sees "α-posterior favours H3" will
interpret it as "the subject uses efficient-CDF-family encoding"
when the honest claim is only "the subject's behaviour is
consistent with α ≈ 2(1+η) *under the Wei-Stocker MI-maximising
encoding assumption*." That's a much narrower claim.

---

## Fool on L21 — the simulator assumes the brain doesn't learn in real time

Prat-Carrabin, Harl & Gershman 2026 is the elephant in the room.
They formulate efficient coding as a property of **gain-adaptive
recurrent network dynamics** — gain modulates on-the-fly as the
network sees new stimuli. The simulator assumes static tuning
curves throughout the session.

Their key quantitative finding: for **narrowly-peaked priors**, the
optimal gain configuration places maximal gains *at some distance
from the prior peak*, yielding "adapter repulsion" — a signature
indistinguishable from BOEC repulsion if you only look at
trial-averaged bias. The simulator's H2/H3/H5 repulsion predictions
could be reproduced by a completely different mechanism: a
classical Bayesian observer with a **gain-adaptive** encoder that
has dynamically configured its gains in response to the recent
prior. Adapter repulsion ≠ BOEC repulsion, but they have the same
first-order behavioural signature.

For our mirror-skew design (ω ≈ 0.34): neither narrowly-peaked nor
wide-uniform. PCHG 2026 predicts a mix of attraction and repulsion
that depends on the within-session gain-adaptation dynamics.

Second elephant: Lieder & Griffiths 2020 (BBS) resource-rational
analysis. The observer uses bounded computation; optimal is given
the resources. In the mirror-skew design, a resource-rational
observer will show biases that depend on ITI (compute time),
cognitive load, and response deadline. The simulator does not vary
these and so cannot disambiguate resource-rational from
unconstrained Bayesian.

Demand: the simulator must admit these as additional unfitted
alternatives beyond the R3 §Models we did not fit block. Extend
that block to cover: (a) BEC, (b) PPC, (c) PCHG 2026 gain-adaptive
recurrent, (d) resource-rational, (e) rational inattention.

---

## Hahn on L19/L21 — identifiability under alternative meta-frameworks

My 2025 identifiability theorem applies to the standard Bayesian
observer model class. It does NOT directly apply to BEC, PPC, or
gain-adaptive recurrent networks. Each of these has its own
identifiability story.

For BEC, identifiability depends on whether the encoder's loss
function is known a priori or fitted. If fitted, the
loss-prior confound from my 2025 Eq. 3 returns with an extra
dimension.

For PPC, the identifiability question is whether the *population-
level likelihood shape* can be recovered from behaviour alone. In
principle yes at infinite trials; in practice likelihood-shape
inference needs large samples.

For gain-adaptive recurrent networks (PCHG 2026), identifiability
is not yet worked out. The dynamical-system parameters (recurrent
weights, gain kinetics, spiking costs) add an entire new parameter
block that current psychophysics data cannot constrain.

The simulator's pre-registration-readiness gaps (R6) already say
the simulator is Stage 1a, not Stage 1b. R7 adds another reason
why: the meta-framework commitment forecloses alternative
identifiability stories that the field is still working out.

Demand: one-line amendment to the §Registered-report readiness
block noting that meta-framework commitment is an additional Stage
1a requirement — explicitly committing to BOEC-within-Wei-Stocker
means the registered report cannot claim "we tested efficient
coding vs alternatives." It can only claim "we tested α-axis
cells within the Wei-Stocker BOEC meta-framework."
