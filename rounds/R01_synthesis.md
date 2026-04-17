# R1 Synthesis

**Inputs**: `references/R01_findings.md`, `rounds/R01_critique.md`.
**Decisions**: accept / reject / defer per critique point, with one-
sentence rationale and proposed simulator amendment where applicable.

---

## Popper — subject-side condition for discriminators (L04)

**Critique**: the discriminator bands in the simulator README hold only
if subjects internalise the mirror-skew prior faithfully, a premise
undermined by Luu-Stocker-Donner 2018, Roach et al. 2016, and
Acerbi 2012.

**Decision**: **ACCEPT** in part. The simulator's veridical-prior
assumption is currently framed as a computational simplification
closing an identifiability confound; R1 evidence shows it is also an
*optimistic* assumption about subject behaviour. Both framings should
coexist — the confound-closure reason (to proceed with HMC) and the
upper-bound reason (real data will show softer signatures than the
simulator predicts).

**Proposed simulator amendment**: in `boec_simulator/README.md`,
extend §"Design axes and closures" subjective-prior bullet to note:
"The veridical-prior assumption is also an *optimistic bound*: Luu et
al. 2018, Roach et al. 2016 and Acerbi 2012 each report subject-side
deviations (prior-width overestimation, partial recalibration, heavy-
tail inflation) that soften the BOEC signature relative to the
predictions shown here. The discriminator bands in §Discriminating
observables should therefore be read as upper bounds on separability;
effective bands in real data are narrower."

**Rejected sub-claim**: Popper's demand for subject-conditional
discriminator bands ("for subjects with $|\alpha^{\mathrm{subj}}| >
2.5$, $\alpha_{\mathrm{sda}} > 0.20$ rejects H2") — defer to HMC
stage. The ex-ante simulator cannot provide these without running
parameter sensitivity sweeps over the subjective-prior axis, which is
exactly what was closed to manage identifiability. That sweep belongs
in a confirmatory study.

---

## Prat-Carrabin — collapse H2/H3/H5 into a 1-parameter family (L05)

**Critique**: H3 and a prior-only anti-Weber observer give different
SD curves *only* because the simulator fixes $\sigma_e = \sigma_0 /
p^{\eta}$ and attributes tail inflation to $\eta > 0$. The two
mechanisms are not discretely separated; they are two points on the
Hahn-Wei 2022 ratio. The simulator's five-cell matrix is category-
theater.

**Decision**: **ACCEPT** in principle, **DEFER** the full re-framing.
The argument is correct — H2 is H3 at $\eta = 0$, and a unified
$\mathcal{J} \propto p^{\alpha}$ parameterisation dissolves the
discrete identity of H3 vs. my null. The five-cell matrix does make
sense as a *hypothesis-space skeleton for HMC model selection* but not
as a theoretical claim about distinct mechanisms. The README already
notes H2 = H3|_{η=0} and should go further.

**Proposed simulator amendment**: add a new subsection to
`boec_simulator/README.md` right after §"H2 vs. H3 — measurement space
vs. θ-space", titled "§ The η-axis and its Prat-Carrabin-Woodford
framing", stating:
- H2 and H3 (and by extension H5) are three sampled points on a
  continuous $\alpha$-axis defined by Prat-Carrabin & Woodford (2020),
  where Fisher information scales as $\mathcal{J} \propto p^{\alpha}$.
- H2 corresponds to $\alpha = 2$ (after CDF back-transform),
  H3 to $\alpha = 2(1 + \eta)$, H5 to same under log encoding.
- The three cells are discretisations for *fitting convenience*, not
  three independent mechanisms. The HMC pass should fit $\alpha$ as a
  continuous parameter and treat the $\alpha$-posterior as the
  primary output, with H2 / H3 / H5 cell labels retired in favour of
  continuous inference.

**Deferred**: actually re-parameterising the simulator code to use
$\alpha$ as a continuous free parameter is a simulator-side task that
exceeds this round's scope (theory-only). File as open question:
`open_questions/OPEN_QUESTIONS.md` item Q01.

---

## Ganguli — H6 / H7 are endpoints of the α-axis, not new cells (L06)

**Critique**: H6 (power-law encoding) and H7 (prior-only anti-Weber)
are not new cells — H7 is $\alpha = 0$ and H6 is a specific $(q,
\beta)$ slot on the same continuous family. The simulator should have
an explicit $\alpha = 0$ point as the efficient-coding-family null.

**Decision**: **ACCEPT**. This is the cleanest resolution of the R1
L01 candidate-cell question. Adding H6 and H7 as discrete cells was
already flagged as a closest-miss concern; framing them as endpoints
of the same $\alpha$-axis eliminates the discreteness altogether. The
simulator amendment proposed above under Prat-Carrabin already covers
H6/H7: the $\alpha = 0$ endpoint IS H7, and Cicchini-Anobile-Burr 2014
$q \approx 0.5$ corresponds to a specific $\alpha$ in the
efficient-coding-family. Do not add discrete H6 / H7 cells; retire
that proposal in favour of the continuous $\alpha$-axis.

**Proposed simulator amendment**: in §"Why five cells, not nine?",
retire the paragraph announcing H6 / H7 as candidates. Replace with a
single paragraph stating that candidate cells H6 and H7 have been
subsumed into the continuous $\alpha$-axis framing (see preceding
subsection), which covers both endpoints plus the
Cicchini-Anobile-Burr empirical case $q \approx 0.5$.

---

## Summary of R1 outcomes

### Accepted amendments to `boec_simulator/README.md`

1. §"Design axes and closures" — subjective-prior bullet: add the
   upper-bound caveat (Luu, Roach, Acerbi).
2. New subsection §"The η-axis and its Prat-Carrabin-Woodford
   framing" — collapse H2/H3/H5 into a continuous $\alpha$-axis with
   named sample points.
3. §"Why five cells, not nine?" — retire H6/H7-as-cells proposal;
   redirect to the $\alpha$-axis subsection.

Cross-reference each simulator commit back to this synthesis document.

### Deferred questions (filed as `OPEN_QUESTIONS.md`)

- **Q01**: simulator code re-parameterisation to use continuous
  $\alpha$ instead of discrete η at {0, 1/3, 1}.
- **Q02**: a sensitivity sweep over $\alpha^{\mathrm{subj}} /
  \alpha^{\mathrm{obj}}$ for Popper's subject-conditional bands.
- **Q03**: whether Fritsche et al. 2020's decoupled encoding-prior /
  decoding-prior formulation should be admitted in a later round.

### Retired lenses

- L04 (design-prediction circularity), L05 (theoretical coherence),
  L06 (H6/H7) — retired from the active backlog. Move to "Completed"
  in `open_questions/LENSES.md`.

### Next round

R2 picks up from L07 (identifiability vs. practical sample size) and
L14 (Hahn-Wei 2022 P/P ratio as a primary discriminator). Both lenses
ride on the $\alpha$-axis re-framing just accepted.
