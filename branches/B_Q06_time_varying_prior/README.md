# B_Q06 — Time-varying prior branch

**Parent question (from main loop)**: Q06 — subjective prior is
non-stationary within a duration-reproduction session (Sohn-Lee
2013 prior-width shrinks; Narain et al. 2018 asymmetric wide↔narrow
learning; Roach et al. 2016 tens-of-trials learning;
Wang-Luo-Ivry et al. 2023 multi-timescale adaptation). A stationary-
prior HMC fits a time-average of the learning trajectory. How does
this time-averaging contaminate the α_sda estimate, and can it be
separated from encoding-driven SD inflation?

**Harness pattern**: pipeline.
- **Stage 1**: characterise the prior-learning trajectory from
  published time-interval studies (Sohn-Lee 2013 rate; Narain 2018
  asymmetry; Roach 2016 timescale).
- **Stage 2**: derive a formal decomposition —
  α_sda observed = α_sda encoding-driven + α_sda learning-driven.
- **Stage 3**: propose sliding-window fit or drift-parameterisation
  as the decontamination method.

## Scope

**In scope**:
- Prior-learning dynamics specific to duration reproduction at
  N ≈ 700 trials per session.
- How the time-averaging bias shifts α_sda estimates.
- Decontamination methods from the literature (sliding window,
  linear-drift prior width, latent-variable HMC).

**Out of scope**:
- Cross-modality prior-learning (Roach 2016 generalisation).
- Explicit prior instruction (Thakur et al. 2021 implicit/explicit).
- Simulator code implementation of a time-varying prior (simulator-
  code task).

## Round plan (capped at 5)

| Round | Focus | Deliverable |
|---|---|---|
| B6R1 | Pipeline stage 1: learning-trajectory characterisation | `round01_trajectory.md` |
| B6R2 | Pipeline stage 2: α_sda decomposition (encoding vs learning) | `round02_decomposition.md` |
| B6R3 | Pipeline stage 3: decontamination method survey | `round03_decontamination.md` |
| B6R4 | Consistency cross-check against B_Q05 (power) and B_Q09 (SD) | `round04_crosscheck.md` |
| B6R5 | Final recommendation for HMC design | `round05_final.md` |

## K-Dense prompt

See `k_dense_prompt.md`.

## Cross-branch pointers

- B_Q05 status: _pending_
- B_Q09 status: _pending_
