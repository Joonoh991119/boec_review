# R2 Critique — three personas

**Lenses**: L07 (identifiability vs. practical sample size), L14 (Q(θ)
P/P ratio as primary discriminator).

**Personas**: Hahn (L07 — identifiability theory), Quine (L14 — holistic
confirmation), Popper (L14 — falsifiability of Q(θ)).

Each critique draws on `references/R02_findings.md` and reaches beyond
the 8-anchor list to recent methodological literatures surfaced in R2.

---

## Hahn on L07 — identifiability is conditional on multi-noise data

The simulator cites my 2025 Theorem 3 for identifiability and then
proceeds as if the guarantee automatically transfers to the
mirror-skew duration-reproduction design. It does not.

Theorem 3 requires response distributions collected at **multiple
small sensory-noise levels**, and the proof mechanism is the
second-order, nonlinear scaling of bias with σ. The present design
has one effective σ per subject (internal timing noise is a fixed
unknown) and two prior shapes. That is multi-prior-shape data, not
multi-noise data. My §2.4 discusses multi-context adaptation as a
partial escape for the Weber + log-prior exceptional-degeneracy
case, but the escape there requires both encoding **and** subjective
prior to adapt to the context — under a short mirror-skew session
only the subjective prior plausibly adapts (if at all; see R1 L04
findings on partial recalibration), while the encoding $f$ is
carried across conditions by assumption. The escape is therefore
partial in principle and weaker still in practice.

Two consequences the simulator must state plainly:

1. The closure assumptions (veridical prior, BLS loss) are doing
   identifiability work. If they fail, the loss-prior confound in my
   Eq. 3 reopens and per-subject posteriors will be broad.
2. What IS identifiable at realistic trial counts (Manning, Prat-
   Carrabin & Woodford 2023 recommend ≥ 500 trials/subject/condition;
   Acerbi 2012 used ≈ 2,700; Hahn-Wei 2024 used up to 10,000) is a
   hierarchical Bayesian fit where **group-level** parameters have
   tight posteriors and per-subject parameters have partially
   pooled posteriors. The simulator's framing of "recover individual
   (σ_e, subjective prior)" is too optimistic for 30 × 700 trial
   counts.

The simulator's Discriminators table implicitly speaks at the subject
level. At this sample size the table must be re-anchored at the
group level, with honest posterior-breadth reporting at the subject
level.

---

## Quine on L14 — Q(θ) replaces observable bundles with a single confound

The pre-R1 simulator carried two primary discriminators
((b_R, b_L) at θ = 1.1 and α_sda). The R1 synthesis collapsed three
hypotheses into a continuous α-axis. R2 now proposes promoting Q(θ)
to a primary discriminator. That progression collapses the
observable space faster than it maps it.

Holistic confirmation: no observable tests a single hypothesis. When
the simulator replaces a tuple (b_R, b_L) with a scalar Q-integral,
it buries the auxiliary assumptions (Gaussian encoding noise,
veridical prior, uniform stakes, BLS readout, stationary prior) that
must hold for Q(θ) to predict bias sign. Q(θ) is not a model-free
observable; it is a model-*conditional* summary statistic. If a
subject's Q-integral disagrees with the bias-sign pattern in their
data, the implication is ambiguous across multiple auxiliary
failures.

Popper will demand rejection thresholds for Q(θ). The Quinean reply
is that those thresholds do not exist in isolation: they are
thresholds *on a bundle* (Q-integral assuming Gaussian noise,
assuming veridical prior, assuming BLS, assuming no motor noise).
Each auxiliary is an open question the simulator already defers
(Q02, Q03). A simulator that headlines Q(θ) while deferring the
auxiliaries is making a commitment that the bundle is stable enough
to report a scalar.

This is not a rejection; it is a demand for bundle declaration. If
Q(θ) is promoted, the simulator must state alongside it the bundle
of auxiliaries that Q(θ) rests on, and flag each bundle member's
empirical support strength.

---

## Popper on L14 — falsifiability of Q(θ) as a discriminator

A sign-predicting observable is inert until a rejection threshold
is attached. The R2 finding that Hahn-Wei 2024's Fig. 7 shows
repulsion larger in circular datasets and smaller in scalar
(numerosity, time) datasets is load-bearing for this lens: in the
time domain specifically, the published empirical ratio rule says
**attraction dominates**. For the simulator to use Q(θ) as a
discriminator between H2/H3/H5 (BOEC family, repulsion-direction)
and H1/H4 (classical family, attraction-direction), it must be
possible for the time-domain Q-integral to come out repulsive.
Hahn-Wei 2024 suggest it usually does not.

Two Popperian demands:

1. State the rejection threshold on the Q-integral explicitly. For
   example: "If the subject's integrated Q(θ) over [0.6, 1.6] s,
   weighted by the experimental prior, has sign opposite to the
   group-level sign with |Z| > 2, the subject rejects the
   majority-family assignment." Without this, promoting Q(θ) is
   decoration.
2. Commit in advance to a time-domain prior on the Q-integral's
   sign. Hahn-Wei 2024 Fig. 7 predicts attraction-dominant. If the
   simulator's BOEC-family predictions (H2/H3/H5) assign a Q-integral
   of the opposite sign, those cells are asking the data to contradict
   the published pattern. That is falsifiable — but then the
   rejection threshold must be stated up front, before the data come
   in.

If the simulator cannot commit to rejection thresholds for Q(θ), it
should not be a primary discriminator. It is still a useful
*interpretive* scalar, but listing it next to α_sda under
"Discriminating observables" without thresholds is category error.
