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
