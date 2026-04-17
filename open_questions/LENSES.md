# Review lenses — rotating backlog

Each round of the loop picks one or two lenses from this list. A lens is
retired from rotation once a round has been committed against it.

## Completed (boec_simulator R1, migrated into boec_review R0 history)

- L01 — **Inductive bias from the 8 anchor papers.** How each paper's
  framing predetermines the predicted signatures.
- L02 — **Legacy code audit** (applied to boec_simulator only; not a
  theoretical lens).
- L03 — **Metric overfit and falsifiability.** Whether the two primary
  discriminators are selected because H1–H5 differ on them or because
  they are neutrally falsifying.
- L04 — **Design-prediction circularity.** Does the mirror-skew prior
  (α = ±3.3, mean ≈ 1.1 s, SD ≈ 0.22 s) pre-bias the simulator toward
  BOEC-family detection?  **Retired R1** — ACCEPT the optimistic-bound
  concern (see R1 synthesis); subject-side deviations (Luu 2018,
  Roach 2016, Acerbi 2012) soften the predicted signature.
- L05 — **Theoretical coherence across the 8 references.**
  **Retired R1** — ACCEPT the unification argument; H2 / H3 / H5 are
  three sample points on a continuous α-axis (Prat-Carrabin-Woodford
  2020) rather than three independent mechanisms.
- L06 — **H6 / H7 candidate assessment.**
  **Retired R1** — ACCEPT Ganguli's framing: H6 / H7 are endpoints of
  the same α-axis; no new discrete cells added.

## Active backlog

- L07 — **Identifiability proofs vs. practical sample size.**
  Hahn-Wang-Wei 2025 proves identifiability under multi-noise-level
  data. The present design has two priors but a single effective noise
  level per subject. Does the identifiability guarantee transfer?
- L08 — **Experimental-parameter sensitivity.** Mirror-skew α choice,
  prior SD, and theta range: which combinations collapse vs. preserve
  H1–H5 separability? Robustness audit of the experimental design.
- L09 — **Reference-paper reproduction honesty.** The simulator
  embeds `reproduce_stocker_simoncelli_fig4.png`, `reproduce_wei_stocker_fig4.png`,
  `reproduce_acerbi_fig1.png`. Are the reproductions faithful in
  assumptions or silently re-parametrised? Audit the reproduction code.
- L10 — **Generative-model assumption audit.** The BLS observer
  assumes (i) Gaussian encoding noise in m-space, (ii) veridical prior,
  (iii) no motor noise, (iv) no attention lapses, (v) no trial-to-trial
  adaptation. Each assumption is a modelling choice that could be
  relaxed.
- L11 — **Empirical precedent for efficient-CDF encoding in timing.**
  Wei-Stocker 2015 used orientation data. Has anyone demonstrated the
  same encoding in interval-timing tasks, or is H2/H3 a direct port
  without empirical backing in the domain?
- L12 — **Alternative observer frameworks.** Sequential-sampling /
  drift-diffusion accounts of duration reproduction, log-normal
  Bayesian observers (Jazayeri-Shadlen), reinforcement-learning
  accounts. Should any be cells of their own, or parametric variants?
- L13 — **Prior-learning dynamics.** The simulator assumes a stationary
  subjective prior. Empirical evidence on the time course of
  prior-learning in mirror-skew designs is sparse; does this matter
  for MCMC?
- L14 — **Hahn-Wei 2022 P/P ratio as a summary statistic.** The
  additive-decomposition framework reduces bias direction to a single
  ratio Q(θ). Should the simulator promote Q(θ) to a primary
  discriminator alongside (bias-sign, α_sda)?
- L15 — **Confounders in the mirror-skew design.** Stimulus order,
  adaptation, response mapping. Do any erase the bias-sign signature?
