# R0 — Loop setup and migration of prior work

**Date**: 2026-04-18.
**Status**: complete.
**Upstream reference**:
[boec_simulator commit 25143b0](https://github.com/Joonoh991119/boec_simulator/commit/25143b0).

## What this round does

Initialises the theoretical-review repo and migrates the already-completed
Round-1 outcomes from `boec_simulator` into the new audit trail.

Directory skeleton, persona roster, lens backlog, and README (mission +
loop protocol) are committed. No new theoretical content.

## Migrated from boec_simulator R1

The simulator already underwent one round of autonomous review against
three lenses before this repo existed. That round is recorded here for
continuity; the amendments it produced have already been applied in the
simulator repo.

### Lens L01 — Inductive bias from the 8 anchor papers
Found that H2's opposite-sign S-shape is the Wei-Stocker 2015 derivation
numerically re-instantiated (parameterisation, not prediction), and
similarly that H3's α_sda ≈ 1+η is a restatement of the σ_e = σ_0/p^η
definition given f' = k·p. H4 inherits Prat-Carrabin 2024's claim that
Fechner-log + constant precision mimics Weber. H5 sits "between H2/H3
and H1/H4" because Hahn-Wei 2022's additive decomposition is used to
narrate direction. Two un-implemented candidates flagged: H6 (power-law
encoding f ∝ θ^q, Stocker-Simoncelli 2006 speed case) and H7 (linear
+ constant + subjective-skewed-prior, Prat-Carrabin 2024 prior-only
anti-Weber).

Amendment: new simulator README §"Known circularities and inductive
biases".

### Lens L02 — Legacy code audit
Classified 60 files in boec_simulator as ACTIVE / LEGACY / DEAD. Deleted
21 DEAD files (diagnostic scripts with no callers, AI-render orphans,
regression fixtures, truncation-sweep outputs, old schematic PNG).
LEGACY files (P1–P5 Priority drivers, R1–R7 precision scripts, dual_app
PNGs) kept as historical record; referenced only from MIGRATION.md.

### Lens L03 — Metric overfit and falsifiability
Found that θ = 1.1 is load-bearing because H1..H5 were defined to differ
there; that α_sda circularly regresses log-SD on -log p assuming the
BOEC functional form; that the two-scalar cell assignment partitions
hypothesis space not observable space. Degeneracy zones not previously
disclosed: H2↔H3 at η<0.2, H4↔H5 at η<0.3, H1↔H5 at small η. R5
posterior-shape correction can shrink observed α_sda by ~2× at
realistic within-subject noise.

Amendment: new simulator README §"Degeneracy matrix".

## Lenses still in rotation

See `open_questions/LENSES.md`. L04 through L15.

## Tools added to the loop

Starting R1 (this repo), rounds draw on three external resources:

- **K-Dense Web** — for cross-disciplinary deep research and synthesis.
- **Web search** — for claim verification and recent literature.
- **Zotero** via MCP — for the personal BOEC / Bayesian-observer /
  psychophysics library and its annotations.

Raw notes from those passes land in `references/RN_findings.md`.

## Next

R1 picks up from L04 (design-prediction circularity), L05 (theoretical
coherence across the 8 refs), and L06 (H6/H7 candidate assessment).
