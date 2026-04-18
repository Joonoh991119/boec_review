# R5 Synthesis

**Inputs**: `references/R05_findings.md`, `rounds/R05_critique.md`.

---

## Acerbi — reproduction-figure captions are soft (L09)

**Decision**: **ACCEPT**. The `reproduce_*.png` figures show pipeline
sanity checks under the simulator's assumptions, not faithful
replications of the source papers.

**Simulator amendment**: extend §Reference-paper reproductions
caption to:

> "These reproductions demonstrate that the simulator's BLS
> observer, when configured with the encoding / noise / prior of
> each source paper's framework, produces signatures qualitatively
> consistent with the published results. They do NOT use the
> original papers' fitted parameters or raw data: the Wei-Stocker
> 2015 figure uses a generic skew-normal prior rather than the
> Girshick et al. 2011 orientation statistics; the
> Stocker-Simoncelli 2006 figure uses a representative contrast
> rather than the full contrast grid; the Acerbi 2012 figure
> matches the factorial structure. The label 'reproduces' is a
> statement about mathematical pipeline fidelity, not about
> data-level replication. The Stocker-Simoncelli 2006 prior is
> itself contested in the field (Hedges et al. 2011; Sotiropoulos
> et al. 2014; Jogan & Stocker 2015; Zhang-Stocker 2021
> reformulates)."

---

## Hahn — anchor-paper replication-status table (L18)

**Decision**: **ACCEPT**. The 8-anchor set has non-uniform
replication status; this must be visible to readers.

**Simulator amendment**: after the Reference papers list, add
§"Anchor-paper replication status" with classification table:

| Anchor | Status | Field-internal critique |
|---|---|---|
| Stocker-Simoncelli 2006 | Classical; widely cited | Prior recovery contested (Hedges 2011; Sotiropoulos 2014; Jogan-Stocker 2015); Zhang-Stocker 2021 reformulates |
| Jazayeri-Shadlen 2010 | Classical; robustly replicated | Narain 2018, Wang-Narain 2018, Ren et al. 2022 TICS |
| Acerbi 2012 | Classical; extended in timing | Sohn-Lee 2013, Wang-Luo-Ivry 2023, Bévalot-Meyniel 2023 |
| Wei-Stocker 2015 | Classical; replicated for orientation | Taylor-Bays 2018; Fritsche 2020; Noel et al. 2021; **efficient-CDF in timing NOT tested** (R3 L11) |
| Wei-Stocker 2016 | Theory; no direct replication | — |
| Hahn-Wei 2022 / 2024 | Recently published; few independent replications | HW2022 preprint → Nat. Neurosci. 2024; < 2 years |
| Hahn-Wang-Wei 2025 | Preprint; no replications | Formal response to the Wei-Stocker identifiability critique |
| Prat-Carrabin-Gershman 2025 | Recent preregistered; no independent replication | Prat-Carrabin-Woodford 2020 precursor |

The simulator should cross-reference this table whenever a
discriminator band cites a specific anchor: "α_sda = 1 + η
(Wei-Stocker 2015 derivation)" should carry the anchor's
replication status so readers can calibrate their confidence.

---

## Fool — iid-trials auxiliary must be in Bundle B (L15)

**Decision**: **ACCEPT**. Serial dependence is the dominant
within-task confounder in duration reproduction and the simulator
implicitly assumes iid trials.

**Simulator amendment**: extend Bundle B (added in R4) with item 8:

> "(viii) **IID trials** — no serial dependence, no trial-order
> effects, no motor-response carryover. Empirically violated in
> duration reproduction: sensory carryover (Cicchini-Mikellidou-
> Burr 2018); decisional carryover (Li-Wang-Zaidel 2026);
> motor-response coupling (Wu et al. 2024); task-switching
> amplification (Cheng-Chen-Yang-Shi 2024); post-perceptual
> emergence (Bliss-Sun-D'Esposito 2017; Pascucci et al. 2023).
> Manassi-Murai-Whitney 2023 meta-analysis confirms robustness
> of serial dependence across modalities. If trials are
> randomly interleaved between A and R conditions, the (b_A,
> b_R) sign pattern is attenuated by sequential carryover from
> the prior trial's condition. If trials are condition-blocked,
> within-block carryover persists but does not cross-contaminate
> — this is the design choice the simulator's discriminators
> implicitly assume."

Also file Q09:

> Q09 — serial-dependence simulation. Add a cell to the simulator
> that models trial-to-trial updating of $p^{\mathrm{subj}}$ by
> the previous response (Wu et al. 2024 motor-coupled update
> rule) and report how much the (b_A, b_R) sign contrast is
> attenuated for interleaved vs. blocked A/R designs. Simulator
> code task, deferred.

---

## Summary of R5 amendments

### Accepted (applied to boec_simulator parallel commit)

1. §Reference-paper reproductions caption extended with "pipeline
   fidelity, not data-level replication" explicit statement and
   per-figure assumption differences.
2. New §Anchor-paper replication status table after References.
3. Bundle B extended with item (viii) IID trials; extensive serial-
   dependence citation block.

### Deferred

- Q09 — serial-dependence simulation cell. Simulator code task.

### Retired lenses

- L09, L15, L18 move to Completed in LENSES.md. All 15 originally-
  enumerated lenses now retired across R1-R5; L16-L18 additions are
  also retired.

### Widening audit

R5 cites **24 non-anchor refs**. Cumulative R1-R5: approximately 80
non-anchor references engaged across the loop.

### Next round (R6)

All primary lenses retired. Candidates for R6:

- Follow-up on deferred questions: Q05 (HMC sample-size
  simulation), Q06 (time-varying-prior HMC), Q07 (parameter
  sensitivity sweep), Q08 (response-skewness threshold), Q09
  (serial-dependence simulation).
- New lens L19 from R3 L17 remainder: Bayesian Efficient Coding
  (Park-Pillow 2024) and likelihood-shape frameworks — do they
  offer anything beyond the α-axis re-framing?
- New lens L20: consistency audit of the amendments accumulated
  across R1-R5 — do the caveats interact in contradictory ways?
- New lens L21: competing unified accounts — Hahn-Wei 2022
  additive decomposition vs. other unification attempts (e.g.
  Prat-Carrabin-Harl-Gershman 2026 dynamic-network formulation).
- New lens L22: the simulator's H-set as a *pre-registered
  hypothesis document* — does it have sufficient prior
  specification to serve as a registered-report analysis plan?

R6 should prioritise L20 (consistency audit) and L22
(pre-registration readiness) — these integrate the accumulated
amendments rather than opening new frontiers, and close the loop
on what has been added to the simulator across R1-R5.
