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

- L07 — **Identifiability proofs vs. practical sample size.**
  **Retired R2** — ACCEPT. HWW 2025 Theorem 3 requires multi-noise
  data; mirror-skew design provides partial escape only. Hierarchical
  group-level inference is the realistic target.
- L14 — **Hahn-Wei 2022 P/P ratio as primary discriminator.**
  **Retired R2** — ACCEPT in part (Quine bundle declaration) /
  ACCEPT (Popper rejection-threshold demand). Q(θ) remains an
  interpretive scalar with a provisional Z > 2 falsifier, NOT in the
  primary discriminator table.

## Active backlog

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
- L15 — **Confounders in the mirror-skew design.** Stimulus order,
  adaptation, response mapping. Do any erase the bias-sign signature?

## Additions queued (against anchor-paper overfit)

- L16 — **Neural population-code evidence for timing.** The simulator's
  efficient-CDF commitment rests on vision (MT) and orientation (V1)
  neural data. What does the timing literature say at the neural
  population level?
- L17 — **Bayesian-alternative unified accounts.** Beyond Hahn-Wei
  2022 additive decomposition, other unifying frameworks: Bayesian
  Efficient Coding (Park & Pillow 2020), likelihood shape approaches
  (Beck et al.), rational inattention (Woodford). Are any a better
  fit than efficient-coding for timing?
- L18 — **Replication status of the 8 anchor papers.** Has any of
  the 8 been replicated or challenged by independent groups? Any
  null results to consider?
