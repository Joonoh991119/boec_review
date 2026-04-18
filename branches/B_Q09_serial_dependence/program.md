# program.md — B_Q09 serial dependence

(Karpathy `autoresearch` pattern adaptation.)

## Objective

Quantify, in units of `%(b_A − b_R) sign-contrast attenuation`,
how much three serial-dependence mechanisms (sensory carryover,
decisional carryover, motor-response coupling) erode the primary
discriminator under interleaved vs. condition-blocked mirror-skew
designs. Deliver a single design recommendation to the
boec_simulator §Bundle B auxiliary (viii).

## Modify

- `branches/B_Q09_serial_dependence/round0*.md` — findings,
  critique, synthesis as produced each round.
- `branches/B_Q09_serial_dependence/README.md` cross-branch
  pointers.
- If synthesis accepts: **exactly one paragraph** in
  `boec_simulator/README.md` §Auxiliary-assumption bundle item
  (viii) — narrowing the iid-trials caveat into a quantitative
  design recommendation.

## Leave alone

- Bundle B items (i) through (vii) — untouched.
- H1–H5 cell definitions.
- §Parametric commitments, §Meta-framework commitment,
  §Identifiability floor — these are closed from R1–R7.
- 8-anchor reference list — additions allowed, substitutions
  forbidden.

## Evaluation criterion (accept / reject)

**Accept** a round's finding iff:
- ≥ 3 empirical studies with quantitative effect-size
  (Cohen's d, % attenuation, or posterior-width Δ).
- Design recommendation carries a falsifiable threshold (e.g.,
  "interleaved attenuation ≥ 50% of blocked → recommend blocked").
- Delta-check at round's end shows the simulator gains content
  it did not have at round start.

**Reject otherwise**. No middle-ground keep.

## Failure handling

- If fewer than 3 quantitative studies available on a given
  mechanism → collapse that fan-out arm into qualitative prose
  and halve its weight in the synthesis.
- If all three mechanisms produce < 10% attenuation asymmetry
  between interleaved and blocked designs → conclude "serial
  dependence does not discriminate the two designs", recommend
  falling back to cost-based design choice, escalate to user.
- If literature contradicts itself (e.g., Bliss 2017 vs. Cicchini
  2018 on timing of SD emergence) → report both, do not synthesise.

## No help

The branch runs to completion within its 5-round cap without
user consultation. Escalation only at failure-handling boundaries.

## Budget

- Round 1: fan-out external research, ~10 Zotero + WebSearch calls.
- Round 2: 3 persona critiques (paragraph each).
- Round 3: fan-in synthesis, delta-check mandatory.
- Round 4: cross-check against B_Q05 / B_Q06 if those have landed.
- Round 5: finalisation + single-paragraph amendment proposal.

If rounds 1–3 already converge, stop at round 3. Do not pad.

## Karpathy delta check (every round)

End each round document with:

> **Delta**: [simulator's Bundle B item (viii) gains / loses:
> \<content\>, ≥ n quantitative citations.]

If `n < 1` and no structural change: round is a non-improvement;
branch early-exits to writeup.
