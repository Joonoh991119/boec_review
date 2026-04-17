# Open questions

Questions deferred from individual rounds. Each item is small enough to
be picked up by a future round or by the user directly.

---

## From R1

### Q01 — Continuous α-axis re-parameterisation
Re-parameterise the simulator so the BOEC family is a continuous
observer with Fisher information $\mathcal{J} \propto p(\theta)^{\alpha}$,
$\alpha$ a free scalar. H2 is $\alpha = 2$, H3 is $\alpha = 2(1 + \eta)$,
H5 is the same under log encoding. `boec_simulator/tools/
make_fig2_predictions.py` currently treats H2/H3/H5 as discrete cells;
the revision would replace the hard-coded NOISE_LEVELS dict with an
α-grid and produce continuous prediction surfaces in bias(θ) /
SD(θ) × α.

**Status**: deferred — simulator code change is out of scope for the
theoretical-review loop.

### Q02 — Subject-conditional discriminator bands
A Popperian sweep over $\alpha^{\mathrm{subj}} / \alpha^{\mathrm{obj}}$
(subjective vs. objective effective skew) to produce bands of the form
"for subjects with $|\alpha^{\mathrm{subj}}| > k$, discriminator X
rejects hypothesis Y." Closes the gap between the simulator's
veridical-prior predictions and real-subject behaviour (Luu-Stocker-
Donner 2018, Roach et al. 2016, Acerbi 2012).

**Status**: deferred — requires opening the subjective-prior axis
that R0 / R1 closed.

### Q03 — Decoupled encoding-prior / decoding-prior
Fritsche, Spaak & De Lange (2020) show that the prior used to optimise
encoding can differ from the prior used in decoding; Bayesian-observer
literature typically ties them. Should the simulator admit a cell
where these differ?

**Status**: deferred to a later round that picks up L10 (generative-
model assumption audit) or L11 (empirical precedent for efficient-CDF
encoding in timing).

---

## From R2

### Q04 — Q-integral rejection threshold null distribution
A Z > 2 threshold was committed provisionally as a BOEC-family
falsifier on the integrated Q(θ). The null distribution depends on
each auxiliary bundle member (Gaussian noise, veridical prior,
stationary prior, BLS, no motor noise); a systematic sweep under
each failure mode would tighten the threshold.

**Status**: deferred, paired with L10.

### Q05 — hierarchical-HMC power analysis
Under the current experimental design (2 priors × ≈ 700 trials ×
≈ 30 subjects), quantify per-subject posterior breadth vs.
group-level posterior tightness for (i) mean Weber fraction, (ii)
mean α (continuous BOEC-family parameter), (iii) subjective-prior
parameters under partial-veridical relaxations.

**Status**: deferred — likely requires out-of-scope simulation with
synthetic datasets and full HMC fitting, which is simulator-code
work, not theoretical review.

---

## From R3

### Q06 — time-varying prior in HMC
Fit the hierarchical HMC with a time-varying $p^{\mathrm{subj}}(\theta)$
(sliding-window or linear-drift parameterisation on the skew
parameter) to quantify the contribution of within-session prior
learning to α_sda estimates. Sohn-Lee 2013 and Narain 2018 motivate
a prior-width shrinkage dynamic; Roach 2016 motivates a
tens-of-trials learning rate.

**Status**: deferred — simulator code change, out of scope for
theoretical review.

---

## From R4

### Q07 — prior-parameter sensitivity sweep
Sweep (α, ω) over a lattice — α ∈ [±1.5, ±5.0], ω ∈ [0.15, 0.40]
— and re-render bias(θ) / SD(θ) / α_sda predictions. Report the
subset where H1-H5 separability is preserved. Follow Depaoli-Winter-
Visser 2020 or Sridharan-Castiglione 2014 for the sensitivity
method.

**Status**: deferred — simulator code task.

### Q08 — response-skewness auxiliary-violation threshold
Calibrate a threshold |γ(response-distribution skewness)| beyond
which the Gaussian-noise auxiliary (Bundle item i) is violated
strongly enough to invalidate the Wei-Stocker 2016 MI bound. Requires
pilot behavioural data.

**Status**: deferred — empirical calibration.
