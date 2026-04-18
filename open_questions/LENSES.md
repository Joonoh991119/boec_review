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

- L11 — **Empirical precedent for efficient-CDF encoding in timing.**
  **Retired R3** — ACCEPT. No duration-domain neural study has
  documented MT-style log-tiling with prior-CDF density; the
  efficient-CDF commitment is a domain transfer. Simulator now
  states this explicitly in §Working hypotheses preamble.
- L12 — **Alternative observer frameworks.**
  **Retired R3** — ACCEPT. Simulator adds §'Models we did not fit'
  naming TDDM (Simen 2013), population clock (Paton-Buonomano
  2018), rational inattention (Woodford 2020) as unfitted
  alternatives; HMC conclusions conditional on Bayesian meta-model.
- L13 — **Prior-learning dynamics.**
  **Retired R3** — ACCEPT. Stationary-prior assumption violated
  by Sohn-Lee 2013, Narain 2018, Roach 2016, Wang-Luo-Ivry 2023.
  Simulator adds stationarity caveat in §Design axes and closures.
- L16 — **Neural population-code evidence for timing.**
  **Retired R3** — covered by L11.
- L17 — **Bayesian-alternative unified accounts.**
  **Retired R3 (partial)** — covered by L12 (TDDM, population
  clock, rational inattention); Bayesian Efficient Coding (Park &
  Pillow 2020) and likelihood-shape approaches still pending, to
  be revisited if a future round picks them up.

- L08 — **Experimental-parameter sensitivity.**
  **Retired R4** — ACCEPT. (α = ±3.3, ω = 0.3374) is a commitment,
  not a theoretical prescription; simulator now frames the choice
  this way and flags the (α × ω) sensitivity sweep + log-uniform
  spacing as Q07 / design-alternative section.
- L10 — **Generative-model assumption audit.**
  **Retired R4** — ACCEPT. Seven auxiliaries consolidated into
  Bundle B in simulator README; Gaussian behavioural-noise defence
  cited via Keemink 2018 / Park-Pillow 2024 / Prat-Carrabin-Harl-
  Gershman 2026.

## Active backlog

- L09 — **Reference-paper reproduction honesty.**
  **Retired R5** — ACCEPT. Figure captions now explicitly state
  "pipeline-fidelity sanity check, not data-level replication";
  per-figure assumption differences listed; Stocker-Simoncelli
  2006 prior contestation flagged.
- L15 — **Confounders in the mirror-skew design.**
  **Retired R5** — ACCEPT. Serial dependence is a dominant within-
  task confounder (Cicchini-Mikellidou-Burr 2018, Li-Wang-Zaidel
  2026, Wu et al. 2024, Manassi-Murai-Whitney 2023). iid-trials
  added to Bundle B as item (viii); Q09 filed.
- L18 — **Replication status of the 8 anchor papers.**
  **Retired R5** — ACCEPT. Anchor-paper replication-status table
  added to simulator; non-uniform status classifying classical-
  robust vs. classical-contested vs. recent-unreplicated vs.
  theory-only.

## Completed by R6

- L20 — **Consistency audit across R1-R5 amendments.**
  **Retired R6** — ACCEPT. No contradictions; three consolidation
  opportunities addressed: §Parametric commitments block added,
  α-axis / H-cell notation clarification added.
- L22 — **Pre-registration readiness.**
  **Retired R6** — ACCEPT. Simulator is Stage 1a (hypothesis
  specification) but not Stage 1b (full analysis plan).
  §Registered-report readiness and gaps block added listing 7
  items a downstream protocol repo must provide.

## R7+ candidates

- L19 — **Bayesian Efficient Coding and likelihood-shape
  frameworks.** Park & Pillow 2024; Beck et al. PPC tradition.
  Do these offer anything beyond the α-axis re-framing from R1?
- L21 — **Competing unified accounts.** Prat-Carrabin-Harl-
  Gershman 2026 dynamic-network formulation as an alternative
  unifying meta-framework to Hahn-Wei 2022 additive decomposition.
