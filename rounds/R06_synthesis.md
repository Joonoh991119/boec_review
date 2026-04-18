# R6 Synthesis

---

## Quine — no contradictions; three consolidation opportunities (L20)

**Decision**: **ACCEPT**. No pair of R1-R5 amendments directly
contradicts another, but the reader load from scattered caveats is
real.

**Simulator amendment**: add a short §"Parametric commitments" block
at the top of the README (between §Scope and §Hypothesis
derivation) that consolidates the simulator's fixed choices in one
place:

> **Parametric commitments (as of boec_review R1-R6).** This
> simulator has committed to:
> - Priors: skew-normal mirror pair ($\alpha = \pm 3.3$,
>   $\omega = 0.3374$, mean $\approx 1.1$ s, SD $\approx 0.22$ s).
>   Parameter choice is an inherited default (see §Design axes).
> - Subjective = objective prior (operational closure; caveat in
>   §Design axes).
> - Stationary subjective prior (caveat in §Design axes).
> - Loss = BLS / $L^2$ (closure in §Design axes).
> - Gaussian additive encoding noise in m-space (Bundle B item i).
> - No motor noise, no lapse rate, iid trials (Bundle B items iv,
>   v, viii).
> - Bias / SD predictions as small-noise expansion (Bundle B item
>   vii).
>
> Each commitment is audited in detail by the corresponding round
> of `boec_review`. Readers disagreeing with a commitment can find
> the round's rationale at
> https://github.com/Joonoh991119/boec_review/tree/main/rounds.

Additionally, insert a one-liner in §The η-axis and its Prat-
Carrabin-Woodford framing clarifying: "H2/H3/H5 are cell labels for
anchor-paper traceability; the underlying mathematical object is
the continuous α. A future HMC pass fits α; the cell labels carry
no independent theoretical commitment beyond anchor citations."

---

## Popper — registered-report gaps (L22)

**Decision**: **ACCEPT**. The simulator is registrable as a Stage
1a (hypothesis space) but not Stage 1b (full analysis plan). The
gaps must be enumerated.

**Simulator amendment**: add §"Registered-report readiness and
gaps" between §Anchor-paper replication status and §Further
reading:

> This simulator constitutes the **hypothesis-space half** of a
> potential registered report: it specifies H1-H5 cells, the
> α-axis continuum, the Bundle B auxiliaries, and the
> discriminator bands that separate the cells. It does NOT
> constitute a complete registered-report document.
>
> **What a downstream experimental-protocol repo must add before
> registration**:
>
> 1. **Subject-level critical values** for each discriminator. Example:
>    "Reject H1 classical if $b(\theta = 1.1)$ has sign inconsistent
>    with the majority for more than 40% of subjects at group-level
>    Z > 2." Current simulator has bands at the family level only.
> 2. **Formal power analysis** (Q05 in boec_review) — synthetic-
>    data HMC at planned (subjects × trials) giving posterior-
>    width estimates on $\alpha$ and group-mean $\sigma_e$.
> 3. **Analysis sequence** — ordered discriminator application,
>    contingencies, multiple-comparison correction.
> 4. **HMC specifics** — prior distributions on subject-level and
>    group-level parameters, NUTS hyperparameters, R̂ / ESS
>    thresholds, posterior predictive check protocol.
> 5. **Model comparison** — WAIC / LOO / Bayes factor method, and
>    the threshold ($\Delta$WAIC > 4? BF > 10?) for rejection.
> 6. **Exclusion criteria** — lapse-rate threshold, timing-range
>    outliers, within-session drift threshold.
> 7. **Plate diagram** of the hierarchical Bayesian model.
>
> Items 1-7 are the job of a sister repository ("boec_protocol" or
> similar) at the experimental-design stage. boec_review Q05, Q07,
> Q09 correspond to items 2, 3, 4 above respectively.

---

## Hahn — partial readiness; Q05/Q07/Q09 gate full registration

**Decision**: **ACCEPT** — but reflected as a status annotation
rather than a new section. The simulator already acknowledges Q05
and Q07 as deferred.

**Simulator amendment**: no new section. Instead, append a
sentence to the §Registered-report readiness gaps block above:

> "boec_review open questions Q05 (hierarchical-HMC power
> analysis), Q07 (parameter sensitivity sweep), Q08 (response-
> skewness auxiliary threshold), and Q09 (serial-dependence
> simulation) are the specific gate conditions for moving from
> Stage 1a (hypothesis specification) to Stage 1b (full analysis
> plan). Until those are executed, the simulator is a partial
> registered-report document."

---

## Summary of R6 amendments

### Accepted (applied to boec_simulator parallel commit)

1. New §Parametric commitments block at the top of the README —
   consolidates scattered commitments in one place.
2. One-sentence clarification in §The η-axis subsection: H2/H3/H5
   are cell labels, not discrete mechanisms.
3. New §Registered-report readiness and gaps block listing 7
   items a downstream protocol repo must add; Q05/Q07/Q08/Q09
   named as gate conditions.

### Retired lenses

- L20, L22 move to Completed.

### Next round (R7) — queue

Primary remaining:
- L19 Bayesian Efficient Coding (Park-Pillow 2024) and likelihood-
  shape frameworks — a meta-framework comparison.
- L21 Competing unified accounts — Prat-Carrabin-Harl-Gershman 2026
  dynamic recurrent-network formulation as alternative to Hahn-Wei
  2022 additive decomposition.

R7 should pair these two: both are "alternative unifying accounts"
lenses that extend the R3 L12 question but focus on non-efficient-
coding or dynamical-system Bayesian observers.
