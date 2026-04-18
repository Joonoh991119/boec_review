# R6 Critique — three personas

**Lenses**: L20 consistency (Quine) · L22 pre-registration readiness
(Popper, Hahn).

---

## Quine on L20 — amendments overlap but do not contradict

I have been auditing the bundle since R2. Across R1-R5 the simulator
has accumulated ~15 discrete caveats, headers, and tables. They
do NOT contradict each other, but they overlap in distracting ways,
and a reader following a specific claim back to its source has to
traverse multiple amendments.

Three overlap zones deserve consolidation:

1. **"Veridical prior" is four things in four places**: (a)
   operational closure required for HWW 2025 identifiability;
   (b) optimistic upper-bound caveat for real-subject behaviour
   (R1 Luu/Roach/Acerbi); (c) stationarity caveat for within-session
   prior learning (R3 Sohn-Lee/Narain); (d) parameter commitment
   sub-text in the prior bullet of Design axes (R4). Each of these
   is correct; they are read as one bullet and one sub-caveat in
   the current README, but a pre-registration user needs them
   organised as: "the veridical assumption has [operational] +
   [empirical] + [temporal] dimensions, all of which must hold for
   the discriminator bands below."

2. **"α-axis" is a reframing of H2/H3/H5 but the H-cell notation
   persists**: Figure 2 of the simulator shows H1-H5 as separate
   columns. The α-axis subsection says they are sample points on
   a continuum. These are compatible only if one reads "H2/H3/H5"
   as cell LABELS not cell IDENTITIES. The README does not
   explicitly make this distinction.

3. **"Pre-registered commitment" is implicit but not collected**:
   Parameter commitments (mirror-skew α, ω, θ range, loss = $L^2$,
   subjective = objective, BLS readout, iid trials, no motor noise,
   no lapses) are scattered across Design axes, Identifiability
   floor, Bundle B, and the Reproduction caveat. A single
   "Parametric commitments" block at the top of the README would
   let a reader see exactly what this simulator has committed to
   before they engage with the discriminators.

No contradictions. Multiple opportunities for consolidation.

---

## Popper on L22 — the simulator is not yet registrable

A registered report requires falsification thresholds that are
objective, subject-specific, and agreed in advance. The simulator's
current discriminator bands are conditional and scale-dependent —
good for a theoretical map, insufficient for a registered report.

Three shortfalls:

1. **No subject-level critical values.** For H1, the band is
   "(b_R, b_L) = (−, +) with α_sda ≈ 0." A registered report needs
   "|b(θ = 1.1) − expected | < 2 × SE for at least 70% of subjects"
   — a machine-readable test with a rejection threshold.
2. **No formal power analysis.** Q05 is deferred; without it, the
   "≈ 700 trials × 30 subjects" scale cited in R2 is indicative,
   not a justified sample size for Bayes factor > 10 on H3 vs. H2
   at α_sda.
3. **No analysis sequence.** Which discriminator fires first?
   (b_R, b_L) sign, then α_sda, then Q-integral? If the first test
   rejects the classical family, does the second test condition on
   that? Order and contingency are unspecified.

Registered-report readiness requires adding a §"Registered-report
gaps" to the simulator listing exactly what needs to be added by
the downstream experimental-protocol repo before the hypothesis
document is registrable.

---

## Hahn on L22 — identifiability completeness

I added the prior × loss confound to the simulator's framework.
R2 accepted the caveat that multi-noise data would be needed. R4
added the Bundle B. R5 added iid-trials.

One identifiability completeness gap remains: the simulator does
not state what would constitute *sufficient* identifiability for
HMC at the planned sample size. The README says "group-level
parameters identify at realistic trial counts" but does not say:
given the imposed closures (Bundle B items i-vii) and the violated
assumption (item viii iid-trials), at 700 × 30 data points, what
is the posterior credible interval width on $\alpha$? Without this
number, the simulator is a qualitative framework, not a quantitative
pre-registration.

This is a call for Q05 + Q07 + Q09 to be executed before full
pre-registration. Each of those is a synthetic-data HMC exercise
that would quantify identifiability at the realistic sample size
under one specific violated assumption (Q05 baseline, Q07 parameter
perturbation, Q09 serial dependence).

Until those are done, the simulator can pre-register the *hypothesis
space* but not the *fit expectations*. That is a partial
registered-report status — registrable as Stage 1a (theoretical
motivation + hypothesis enumeration), not Stage 1b (full analysis
plan).
