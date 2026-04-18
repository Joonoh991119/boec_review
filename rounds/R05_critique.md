# R5 Critique — three personas

**Lenses**: L09 reproduction honesty (Acerbi) · L18 replication status
(Hahn) · L15 confounders (Fool).

---

## Acerbi on L09 — what do the reproduce_*.png figures actually prove?

The simulator's README captions the three reproduction figures as
"confirming the numerical pipeline before it is used as a prediction
oracle." This is softer than "replicating the original paper," and
rightly so — but a reader will still read "reproduce" as "match
the published result." That reading is not warranted.

To reproduce Wei-Stocker 2015 Fig. 4 *faithfully* you need:
(i) the Girshick et al. 2011 orientation prior, not a generic
skew-normal;
(ii) the stimulus noise levels the original paper fit (different σ
per contrast condition);
(iii) the same loss-exponent p the paper used (p = 2 standard, but
p = 4 was explored in their extensions);
(iv) a recovery pipeline that matches their numerical grid and
normalisation.

If the simulator's pipeline uses a generic skew-normal prior and a
single σ, the figure shows "the simulator's BLS observer produces a
repulsive S-shape bias under the Wei-Stocker encoding *with
different parameters than the paper used*." That is a pipeline
sanity check, but it is NOT a faithful replication of the
Wei-Stocker 2015 finding on Girshick orientation data.

Two demands:

1. State explicitly in each reproduction-figure caption: "Assumptions
   used: prior = X, encoding = Y, noise = Z. These differ from / match
   the source paper as follows: ..."
2. For the Stocker-Simoncelli 2006 figure specifically, the known
   identifiability critique (Hedges 2011, Sotiropoulos 2014, Jogan &
   Stocker 2015, formalised in Zhang-Stocker 2021) means the
   "reproduced prior" in that original paper is not itself
   well-identified. The reproduction figure inherits this issue.

Without these caveats, a reader who sees "reproduce_wei_stocker_fig4"
will assume the simulator has matched their published result on
their published data. It has not. It has produced a *family-of-
observers demonstration* under the simulator's own assumptions.

---

## Hahn on L18 — anchor papers do not have uniform replication status

The 8 anchors the simulator rests on have highly non-uniform
replication status. Treating them as if they were textbook-
established creates two problems: (i) overweighting recent
preprints whose predictions have not been independently tested;
(ii) under-representing field-internal identifiability critiques.

My 2025 paper (HWW 2025) is itself a FORMAL CRITIQUE of the
identifiability assumptions in the Stocker-Simoncelli / Wei-Stocker
framework — a critique the simulator now cites as an anchor. Good.
But the simulator does not yet carry the complete field-internal
picture:

1. **Stocker-Simoncelli 2006 prior is not itself well-identified.**
   Hedges 2011, Sotiropoulos 2014, Jogan & Stocker 2015 all show
   the reverse-engineered prior is sensitive to the likelihood-form
   assumption. Zhang-Stocker 2021 is the reformulated, tightly-
   constrained version. The simulator cites SS2006 as a foundational
   Bayesian observer reference but never flags that its prior
   recovery is contested. The `reproduce_stocker_simoncelli_fig4.png`
   inherits this contestation.
2. **Recent anchors (HW2024, HWW2025, PCG2025) are NOT independently
   replicated.** The simulator weights them as if they were
   textbook results. A reader of the References section cannot tell
   which anchors are classical-but-contested, classical-and-robust,
   or recent-and-unreplicated. This matters for downstream HMC
   interpretation: if a finding depends on a recent-preprint
   prediction, its confidence should be lower than if it depends
   on a robustly-replicated classical result.
3. **The 8-anchor set is itself a field snapshot.** Five of the
   eight are from one research group ecosystem (Stocker, Wei, Hahn;
   Prat-Carrabin-Gershman is a different group). Three are from
   distinct groups (Jazayeri-Shadlen, Acerbi-Wolpert-Vijayakumar).
   The simulator's theoretical framing inherits the Wei-Stocker
   group's emphasis on efficient coding. Independent replication
   from outside that ecosystem is the missing gate.

Demand: add a §"Anchor-paper replication status" table to the
References section, classifying each anchor as classical-robust,
classical-with-critique, recent-unreplicated, or theory-only.

---

## Fool on L15 — trial-order is the silent variable

Every rejection threshold in the simulator assumes iid trials. That
is never true in duration reproduction experiments. Trial n's
response depends on trial n−1's stimulus (sensory carryover;
Cicchini-Mikellidou-Burr 2018) and on trial n−1's response
(decisional carryover; Li-Wang-Zaidel 2026). These two carryovers
can have opposite signs (Pilly-Seitz 2019 in bisection).

Three ways the mirror-skew design is vulnerable:

1. **Interleaved vs. blocked A/R conditions**: if trials are
   randomly interleaved, an A-condition trial preceded by an R-
   condition trial sees a *different* effective prior than if
   preceded by another A-condition trial. Cheng-Chen-Yang-Shi 2024
   quantify this for reproduction-after-reproduction vs.
   reproduction-after-bisection. The (b_A, b_R) sign pattern the
   simulator predicts assumes condition-blocked analysis with no
   cross-condition carryover.
2. **Motor-response coupling** (Wu et al. 2024): serial dependence
   in timing requires *consistent motor responses*. If the task
   interleaves Go and No-Go trials, or if the response modality
   changes across conditions, serial dependence is gated off. The
   simulator's ramp-to-signature story assumes stable motor
   modality.
3. **Working-memory retention**: Bliss, Sun & D'Esposito (2017)
   and Pascucci et al. (2023) find serial dependence is weak at
   perception but grows with WM retention delay. If the experiment
   uses long ISIs (> 1 s), serial dependence grows; if short ISIs,
   it shrinks. Variable ISI across conditions confounds the
   bias-sign signature.

The simulator has no cell that models trial-sequence dependency.
None of the five hypotheses represents "A BLS observer whose
effective prior updates from trial n−1." That means the HMC will
absorb ALL serial-dependence variance into the per-subject noise
term $\sigma_e$, inflating it artificially and potentially
shifting the α-posterior.

Demand: flag trial-sequence dependency as an auxiliary whose
failure shifts α. Add to Bundle B as item 8: "iid trials (no serial
dependence)." Cite Cicchini-Mikellidou-Burr 2018, Li-Wang-Zaidel
2026, Wu et al. 2024, Manassi-Murai-Whitney 2023 meta-analysis.
