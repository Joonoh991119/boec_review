# B_Q09 — Serial-dependence simulation branch

**Parent question (from main loop)**: Q09 — serial-dependence
simulation. Model trial-to-trial updating of the subjective prior
by the previous response (Wu et al. 2024 motor-coupled update rule)
and quantify how much the (b_A, b_R) sign contrast is attenuated
for **interleaved** vs. **condition-blocked** mirror-skew designs.

**Urgency**: this is the only branch whose outcome directly
constrains the experimental design. If serial dependence erodes the
sign signature in an interleaved design but preserves it in a
blocked design, the experiment should be blocked. Conversely, if
sign preserved in both, interleaved allows more statistical power.

**Harness pattern**: fan-out / fan-in.
- **Fan out**: three parallel reviewer agents on three serial-
  dependence mechanisms — sensory carryover (Cicchini-Mikellidou-
  Burr 2018), decisional carryover (Li-Wang-Zaidel 2026),
  motor-response coupling (Wu et al. 2024).
- **Fan in**: synthesis round combines the three into a single
  design recommendation with quantitative attenuation estimates.

## Scope

**In scope**:
- Serial dependence mechanisms documented in duration reproduction.
- Interleaved vs. blocked A/R design implications for (b_A, b_R)
  sign.
- Quantitative magnitude estimates (what fraction of the sign
  contrast survives?) based on published effect sizes.

**Out of scope**:
- Simulator code implementation of a serial-dependence observer
  (deferred as separate simulator-code task).
- Serial dependence in other tasks (bisection, discrimination).
- Long-timescale adaptation (covered by Q06 branch).

## Round plan (capped at 5)

| Round | Focus | Deliverable |
|---|---|---|
| B9R1 | Fan-out research pass: three SD mechanism reviews | `round01_findings.md` |
| B9R2 | Fan-out persona critique: Cicchini (sensory), Li-Wang-Zaidel (decisional), Wu (motor) | `round02_critique.md` |
| B9R3 | Fan-in synthesis: attenuation estimates per design + recommendation | `round03_synthesis.md` |
| B9R4 | Consistency cross-check against B_Q05 / B_Q06 outputs (if those have rounds in) | `round04_crosscheck.md` |
| B9R5 | Finalisation + simulator amendment proposal | `round05_final.md` |

## K-Dense Web prompt (user-launched)

See `k_dense_prompt.md` in this directory.

## Safety and exit conditions

- If after B9R3 the synthesis is unable to recommend
  interleaved-vs-blocked with attenuation estimates > 30%
  asymmetry between designs, the branch escalates to user: "SD
  cannot discriminate the two designs — other criteria must
  decide."
- If literature depth is insufficient (< 5 quantitative effect-size
  studies), the branch escalates: "Simulation with synthetic SD
  rules is the only way forward — requires simulator code."

## Cross-branch pointers (filled after other branches complete)

- B_Q05 status: _not started_
- B_Q06 status: _not started_
