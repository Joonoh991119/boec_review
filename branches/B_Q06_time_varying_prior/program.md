# program.md — B_Q06 time-varying prior

(Karpathy `autoresearch` pattern adaptation.)

## Objective

Decompose the observed α_sda into `encoding-driven + learning-
driven` components under a non-stationary subjective prior.
Deliver a decontamination rule (method + citation anchors) that
the downstream HMC can apply to separate the two. Quantify the
expected learning-driven α_sda contribution at N ≈ 700 trials
per session in duration reproduction.

## Modify

- `branches/B_Q06_time_varying_prior/round0*.md`.
- `branches/B_Q06_time_varying_prior/README.md` pointers.
- If synthesis accepts: narrow the simulator's §Design axes
  and closures Subjective-prior bullet stationarity caveat
  from a qualitative warning to a quantitative bound ("at 700
  trials, learning-driven α_sda contribution is expected to be
  < x").

## Leave alone

- §Parametric commitments.
- §Bundle B auxiliaries.
- Hahn-Wei 2022 additive decomposition.

## Evaluation criterion

**Accept** iff:
- Pipeline stages 1–3 each reference ≥ 2 empirical timing studies
  for the learning-trajectory characterisation.
- The decontamination rule has at least one published
  implementation (sliding-window Sohn-Lee 2013 style; latent
  drift Wang-Luo-Ivry 2023 style; or Bévalot-Meyniel 2023 implicit
  vs. explicit dynamics).
- Delta-check passes.

**Reject otherwise**.

## Failure handling

- If no paper reports α_sda under time-varying prior explicitly →
  derive an analytical bound from the additive-decomposition
  Q(θ) formula (Hahn-Wei 2022 Eq. 4) and flag as "analytical
  upper bound, no empirical confirmation."
- If decontamination methods are mutually inconsistent →
  report both, recommend user pilot-data to disambiguate.

## No help

Runs within 5-round cap autonomously.

## Budget

- Round 1: trajectory characterisation from Sohn-Lee 2013,
  Narain et al. 2018, Roach et al. 2016, Wang-Luo-Ivry 2023.
- Round 2: α_sda decomposition derivation (Hahn-Wei Q(θ) form).
- Round 3: decontamination method survey.
- Round 4: cross-check against B_Q05 (power) and B_Q09 (SD).
- Round 5: final recommendation.

## Karpathy delta check

> **Delta**: [§Design axes stationarity caveat gains / loses:
> \<content\>, quantitative bound x = \<value\>, ≥ n citations.]

If `n < 2` AND no `x`: branch early-exits.
