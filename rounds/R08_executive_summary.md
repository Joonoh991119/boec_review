# R8 Executive summary

**Purpose**. A lab-external reader can use this 600-word document to
understand the boec_simulator's current status without walking the
R1–R7 audit trail. The full per-round documentation remains at
`rounds/R01_*.md` through `rounds/R07_*.md`; this file is the
self-contained entry point.

## 1. What is the simulator for?

`boec_simulator` (https://github.com/Joonoh991119/boec_simulator) is
an **ex-ante prediction instrument** for a duration-reproduction
psychophysics experiment with two mirror-skew priors (α = ±3.3,
ω = 0.3374). It maps assumption → predicted bias(θ) and SD(θ)
curves for five working hypotheses on the encoding × noise plane:

- **H1** linear × Weber — scalar-variability baseline
- **H2** efficient-CDF × constant — canonical BOEC
- **H3** efficient-CDF × efficient-prior — strong BOEC (η ∈ [1/3, 1])
- **H4** Fechner-log × constant — classical log encoding
- **H5** Fechner-log × efficient-prior — modular BOEC

The simulator does not fit data. Its output informs which cells to
carry into HMC fitting downstream.

## 2. What did the review loop change?

Seven rounds of adversarial review (R1–R7) produced ~100 non-anchor
citations and the following consolidated amendments:

- **R1** H2/H3/H5 reframed as sample points on a continuous α-axis
  (Prat-Carrabin & Woodford 2020, $\mathcal{J} \propto p^{\alpha}$);
  veridical-prior caveat (Luu 2018; Roach 2016; Acerbi 2012);
  H6/H7-as-cells retired.
- **R2** Identifiability-floor block (Hahn-Wang-Wei 2025 Theorem 3
  needs multi-noise data; partial escape only); Q(θ) promoted to an
  interpretive scalar (not a primary discriminator) with Z > 2
  provisional rejection threshold.
- **R3** Efficient-CDF in timing flagged as a domain transfer without
  neural support (Paton-Buonomano 2018 population clocks); §Models
  we did not fit with TDDM, population clock, rational inattention;
  stationarity caveat (Sohn-Lee 2013; Narain 2018; Wang-Luo-Ivry
  2023).
- **R4** Prior-parameter commitment block (Depaoli et al. 2020);
  log-uniform spacing as the H1↔H4 degeneracy resolver; Bundle B of
  seven auxiliaries (Gaussian noise via Keemink 2018, Park-Pillow
  2024, Prat-Carrabin-Harl-Gershman 2026).
- **R5** Reproduction-fidelity caveat (not data replication);
  anchor-paper replication-status table (SS2006 contested; JS2010
  robust; HW2024/HWW2025/PCG2025 unreplicated); Bundle B item
  (viii) iid-trials (Cicchini 2018; Li-Wang-Zaidel 2026; Wu 2024;
  Manassi-Murai-Whitney 2023 meta-analysis).
- **R6** Consolidation — §Parametric commitments unifies ~15
  scattered caveats; §Registered-report readiness lists 7 items a
  downstream protocol repo must add for full RR compliance.
- **R7** §Meta-framework commitment — Wei-Stocker static-MI
  efficient coding is one meta-framework; BEC (Park-Pillow 2024) and
  PPC (Ma et al. 2006) are distinct. Gain-adaptive recurrent
  networks (PCHG 2026) produce "adapter repulsion" mimicking BOEC
  repulsion; resource-rational (Lieder-Griffiths 2020) and rational
  inattention (Woodford 2020) added to the unfitted-alternatives
  block.

## 3. Commitments at a glance

**Parametric** (simulator fixes): skew-normal mirror pair (α = ±3.3,
ω = 0.3374); subjective = objective prior; stationary prior; loss =
BLS/L²; Gaussian additive m-noise; no motor noise / no lapse / iid
trials; small-noise additive-δ; static tuning curves.

**Bundle B** (auxiliaries, 8 items, Bundle B detail in
`boec_simulator/README.md`): Gaussian noise, veridical prior,
stationary prior, no motor noise, no lapse rate, BLS/L²,
additive-on-f, iid trials.

**Meta-framework**: Wei-Stocker-style static-tuning MI-maximising
efficient coding. BEC / PPC / gain-adaptive recurrent / resource-
rational / rational-inattention are NOT tested.

## 4. Open questions (Q01–Q09) — gate conditions for full
registration

- Q01 continuous α-axis re-parameterisation in simulator code.
- Q02 subject-conditional discriminator bands (requires opening
  subjective-prior axis).
- Q03 decoupled encoding-prior / decoding-prior (Fritsche 2020).
- Q04 Q(θ) rejection-threshold null distribution.
- Q05 hierarchical-HMC power analysis (required for Stage 1b RR).
- Q06 time-varying-prior HMC (required for Stage 1b RR).
- Q07 (α, ω) sensitivity sweep (required for Stage 1b RR).
- Q08 response-skewness auxiliary-violation threshold.
- Q09 serial-dependence simulation (required for Stage 1b RR).

Q05, Q06, Q07, Q09 are the four simulator-side tasks that must be
executed before the repo can serve as a Stage 1b full analysis plan.

## 5. Confidence calibration for a downstream HMC user

- **H-set**: high confidence *within* Wei-Stocker meta-framework;
  low-to-medium confidence outside it. H6/H7 are retired as
  endpoints of the α-axis, not discrete cells.
- **Discriminator bands**: regime-dependent. α_sda for H3 is
  `1 + η` only after the R5 $D_0$ correction; observed slopes may
  shrink by ~2× at realistic within-subject noise. Subject-level
  critical values are NOT provided (Q02).
- **α-posterior interpretation**: behavioural-α, not neural-α. The
  posterior tells you which α-value in the Wei-Stocker family is
  best-supported by the data; it does not tell you about the
  subject's neural encoding scheme nor whether a non-Wei-Stocker
  meta-framework would fit better.

Anchor-paper replication status is in the simulator's §Anchor-paper
replication status table.

---

**Full audit trail**: `boec_review/rounds/R01_synthesis.md` through
`rounds/R07_synthesis.md`. Individual persona critiques at
`rounds/R01_critique.md` through `rounds/R07_critique.md`. External-
research findings with widening citation bibliography at
`references/R01_findings.md` through `references/R07_findings.md`.
