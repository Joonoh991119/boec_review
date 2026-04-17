# R3 Critique — three personas

**Lenses**: L11 empirical precedent for efficient-CDF encoding in
timing · L12 alternative observer frameworks · L13 prior-learning
dynamics.

**Personas**: Acerbi (L11), Fool (L12), Fechner (L13).

---

## Acerbi on L11 — the CDF-encoding claim does not have timing data

As the timing psychophysicist in the roster, I remind the loop that
every assertion about duration perception must be anchored in
duration data, not ported from orientation. Wei-Stocker 2015 used
Girshick et al.'s natural orientation statistics; Zhang-Stocker 2021
used MT speed tuning; both are visual, both low-level. The interval-
timing literature I know — Paton-Buonomano 2018, Matell-Meck 2004,
Narain 2018, Mello-Soares-Paton 2015 — reports a **population clock**:
ramping or sequential activity, not a log-tiling tuning curve allocation
proportional to $\sqrt{p(\theta)}$.

The simulator's H2 / H3 / H5 cells therefore commit to an encoding
scheme that no duration-domain neural study has documented. When a
subject's data favours H3 in an HMC fit, the inference is "the
subject's behaviour is consistent with the Wei-Stocker mathematical
model evaluated on this design" — NOT "the subject uses efficient-
CDF encoding for time." The latter conclusion requires a neural
recording with log-tiling tuning curves and density proportional to
the prior's CDF. Such a recording does not exist for duration.

The simulator should state, in the section introducing H2 / H3 / H5,
that the efficient-CDF encoding is a domain transfer without neural-
level empirical support in timing. This is the honest framing. The
α-axis reinterpretation from R1 already helps: the mathematical family
is what gets fitted, not a specific neural claim. But the $\alpha$-
posterior, when published, must be captioned as "effective
behavioural α in the Wei-Stocker family," not "the subject's
neural-encoding α." Without this caveat, an HMC posterior on $\alpha$
will be over-interpreted.

---

## Fool on L12 — Bayesian monoculture

The 5-cell matrix is incestuous. Every cell is a Bayesian observer;
every bias / SD prediction comes from a posterior. This is how you
get your answer before running the experiment: restrict the model
space to one family and the "best" cell will be in that family.

Interval-timing literature has at least three competing frameworks
that the simulator's HMC will never consider:

1. **Adaptive drift-diffusion (Simen et al. 2013)** — scalar variability
   emerges from network dynamics, not from a posterior. Predicts
   attractive bias of roughly the same shape as BLS + mirror prior.
   If this is the actual mechanism, the HMC will still pick one of
   the 5 cells as "best" — because nothing else is in the space.
2. **Population clocks / ramping codes (Paton-Buonomano 2018,
   Mello-Soares-Paton 2015)** — bias from across-subject variation in
   pacemaker dynamics, not from encoding-precision allocation. This is
   the actual neural-level encoding for time in at least the striatum.
3. **Resource-rational / rational-inattention (Woodford 2020,
   Bhui-Lai-Gershman 2021)** — observer allocates precision to
   minimise expected loss. Equivalent to Bayesian observer only
   under specific loss choices.

The simulator should at minimum add a "§Models we did not fit" section
that names TDDM, population clock, and rational-inattention as
alternative meta-models whose first-order predictions (attractive
S-shape, scalar SD) are similar to the Bayesian observer's. The HMC
conclusions are *conditional on the Bayesian framework* being the
correct meta-model — this is not a "detail" but the most important
caveat.

If you cannot afford to fit alternative frameworks, at least declare
the model-space restriction as a commitment, not a hidden assumption.

---

## Fechner on L13 — the stationary-prior assumption is empirically false

The simulator assumes $p^{\mathrm{subj}}(\theta)$ is constant across
trials within a session. The timing literature says otherwise.
Sohn-Lee 2013 fit a three-parameter Bayesian observer across 10
sessions and recovered a prior width that **shrinks monotonically**
across sessions. Narain et al. 2018 report asymmetric learning
rates: prior updates are slower going wide→narrow than narrow→wide.
Roach et al. 2016 find prior learning on a tens-of-trials timescale.
Wang, Luo, Ivry et al. 2023 argue for a unitary mechanism
integrating local and global statistics. Wiener et al. 2014 and
Cheng-Chen-Shi 2024 document trial-by-trial carryover.

The mirror-skew duration experiment lasts ≈ 700 trials per subject
— longer than Roach's timescale, shorter than Sohn-Lee's. The
subjective prior during trials 1–100 will differ from trials 600–700.
The simulator's HMC fits a single $p^{\mathrm{subj}}(\theta)$. That
fitted quantity is a TIME-AVERAGE of the dynamic prior, not the
prior at any particular trial.

Two consequences:

1. If the behavioural $\alpha_{\mathrm{sda}}$ has a component from
   prior-width shrinkage across trials (early trials: broader prior,
   larger SD; later trials: narrower prior, smaller SD), the fitted
   time-averaged prior will absorb some of this variation, pulling
   $\alpha_{\mathrm{sda}}$ values toward different η estimates
   depending on the fraction of early-learning trials in the sample.
2. Serial-dependence effects (Wiener 2014; Cheng-Chen-Shi 2024)
   will appear as unexplained between-trial variance that the
   per-subject posterior on σ_e must absorb, inflating $\sigma_e$
   estimates.

The simulator needs at least a caveat: subjective-prior stationarity
is an ex-ante assumption; a confirmatory study should fit with a
time-varying prior. Otherwise the HMC $\alpha$-posterior is biased
by the learning trajectory.
