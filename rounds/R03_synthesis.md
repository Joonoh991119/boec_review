# R3 Synthesis

**Inputs**: `references/R03_findings.md`, `rounds/R03_critique.md`.

---

## Acerbi — efficient-CDF encoding is a domain transfer without timing support (L11)

**Decision**: **ACCEPT**. The evidence is stark — no interval-timing
neural study has documented MT-style log-tiling with density
proportional to $\sqrt{p(\theta)}$. The duration domain is a
population-clock (ramping / sequential) regime, not a
Wei-Stocker regime.

**Simulator amendment**: add a paragraph at the top of the §Working
hypotheses section, before H1 introduction:

> "H2 / H3 / H5 inherit the efficient-CDF encoding from Wei-Stocker
> 2015, which was established for orientation (Girshick et al. 2011)
> and extended to speed (Zhang & Stocker 2021) via MT physiology
> (Nover et al. 2005). The interval-timing literature has no
> corresponding empirical precedent: neural recordings report
> population-clock dynamics (Paton & Buonomano 2018, Mello-Soares-
> Paton 2015) rather than a static tuning-curve allocation
> proportional to the prior's CDF. When HMC favours a BOEC cell in
> duration data, the inference is 'subject behaviour is consistent
> with the Wei-Stocker mathematical model', NOT 'the subject uses
> efficient-CDF encoding for time'. The $\alpha$-posterior (see
> §η-axis) is an effective behavioural parameter, not a direct
> neural-encoding claim."

---

## Fool — Bayesian monoculture (L12)

**Decision**: **ACCEPT**. The simulator's HMC will pick a Bayesian
cell because only Bayesian cells are in the space. This is a
pre-commitment, not a discovery.

**Simulator amendment**: add new §"Models we did not fit" between
§Interpretive scalars and §Identifiability. State:

> "The 5-cell matrix is entirely inside the efficient-coding
> Bayesian-observer family. Three alternative meta-models are
> standard in interval-timing literature and are NOT fitted here:
>
> 1. **Adaptive drift-diffusion (TDDM)** — Simen et al. 2013;
>    scalar variability from network dynamics without a posterior.
> 2. **Population clocks / beat-frequency** — Paton & Buonomano
>    2018 review; Matell-Meck 2004 striatal beat-frequency;
>    Mello-Soares-Paton 2015. Scalar variability from accumulated
>    network-dynamics noise.
> 3. **Resource-rational / rational-inattention** — Woodford 2020;
>    Bhui-Lai-Gershman 2021. Equivalent to Bayesian observer only
>    under specific loss choices.
>
> HMC conclusions below are conditional on the Bayesian-observer
> meta-model. A confirmatory study should include at least a TDDM
> comparison cell; the present study cannot adjudicate between
> meta-models."

---

## Fechner — stationary-prior assumption is violated (L13)

**Decision**: **ACCEPT**. Sohn-Lee 2013 (prior shrinks),
Narain 2018 (asymmetric learning rates), Roach 2016 (tens-of-
trials learning), Wang-Luo-Ivry 2023 (multi-timescale adaptation)
jointly establish that the subjective prior is non-stationary in
the mirror-skew duration regime.

**Simulator amendment**: extend the §Design axes and closures
Subjective-prior bullet with a second caveat:

> "Stationarity caveat (boec_review R3): in addition to being an
> optimistic bound (R1), the veridical-prior assumption is also a
> stationarity assumption. Duration-timing prior learning is
> non-stationary within a session (Sohn-Lee 2013: prior width
> shrinks across sessions; Narain 2018: asymmetric learning rates
> wide↔narrow; Roach 2016: partial learning in <1 hour; Wang-Luo-
> Ivry 2023: unitary adaptive mechanism across timescales). The
> fitted $p^{\mathrm{subj}}(\theta)$ in HMC is a time-average over
> the learning trajectory, not the prior at any specific trial.
> $\alpha_{\mathrm{sda}}$ estimates inherit a contribution from
> this time-averaging that must be separated from encoding-
> driven SD inflation in confirmatory analysis."

Also file Q06:

> Q06 — trial-index interaction. Fit the HMC with a time-varying
> prior (e.g. sliding-window ML, or linear drift of skew parameter)
> to quantify within-session prior learning contribution to
> $\alpha_{\mathrm{sda}}$.

---

## Summary of R3 amendments

### Accepted (applied to boec_simulator in parallel commit)

1. Preamble to §Working hypotheses — efficient-CDF encoding in
   timing is a domain transfer without neural support.
2. New §"Models we did not fit" — TDDM, population clock, rational
   inattention as non-Bayesian alternatives.
3. Extended §Design axes and closures Subjective-prior bullet with
   stationarity caveat.

Cross-reference: this synthesis doc.

### Deferred

- Q06 — time-varying prior HMC fit. Simulator code task, deferred.

### Retired lenses

- L11, L12, L13 moved to Completed.

### Widening audit

R3 cited **26 refs outside the 8-anchor set** across three findings
sections. Far above the 5-ref minimum. Papers that entered the
discussion for the first time: Paton-Buonomano 2018 (population
clocks), Mello-Soares-Paton 2015 (striatal population code),
Simen et al. 2013 (TDDM), Matell-Meck 2004 (beat-frequency),
Buhusi-Meck 2005 (interval-timing review), Bhui-Lai-Gershman 2021
(resource-rational), Woodford 2020 (rational inattention),
Wang-Luo-Ivry 2023 (unitary mechanism), Wiener et al. 2014
(carryover), Cheng-Chen-Shi 2024 (sequential biases in time),
Flesch-Saxe-Summerfield 2023 (continual task learning), Nieder 2016
(numerosity logarithmic coding), Wittmann 2009 (time perception
review), Mulder et al. 2012 (DDM with payoff), Ratcliff-McKoon
2008 (DDM foundational), Gu et al. 2025 (attractor dynamics in
estimation), Usher-McClelland 2001 (leaky competing accumulator),
Wong-Wang 2006 (recurrent network decision), Gold-Shadlen 2007
(neural decision review).

### Next round (R4)

Candidates remaining on active backlog:
- L08 experimental-parameter sensitivity
- L09 reference-paper reproduction honesty
- L10 generative-model assumption audit
- L15 confounders in mirror-skew
- L16 neural population-code evidence for timing
  (moved Completed this round via L11)
- L17 Bayesian-alternative unified accounts
  (moved partially Completed this round via L12)
- L18 replication status of the 8 anchor papers

R4 should pick L08 (parameter sensitivity) + L10 (assumption audit).
These are integrative across the R1-R3 amendments already applied.
