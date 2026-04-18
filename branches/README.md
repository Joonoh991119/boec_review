# Branches — deep-dive loops on selected open questions

The R1–R8 loop retired all 22 enumerated lenses and filed 9 open
questions (Q01–Q09). Q05, Q06, Q09 are the three most directly
research-question-relevant items. Each has its own branch here.

Each branch runs a **mini-loop** of 3–5 rounds using the same
protocol as the main loop:
1. External research pass (Zotero MCP + WebSearch; K-Dense Web
   user-launched when applicable).
2. 2–3 specialist persona reviewers from `../reviewers/personas.md`.
3. Synthesis → simulator amendment if accepted; cross-reference
   commit.
4. Commit with `[Bxx Rn]` prefix to this repo.

**Harness pattern per branch** (`skills-repo/harness` taxonomy):

| Branch | Question focus | Harness pattern |
|---|---|---|
| B_Q05_hmc_power | Hierarchical HMC posterior-width at realistic sample size | **generate-and-verify**: synthetic-data HMC producer + validator |
| B_Q06_time_varying_prior | Prior-learning-dynamics contamination of α_sda | **pipeline**: sliding-window fit → drift quantification → decontamination rule |
| B_Q09_serial_dependence | Interleave-vs-block design impact on (b_A, b_R) sign | **fan-out/fan-in**: parallel serial-dep models (sensory, decisional, motor) → consolidated design recommendation |

**Safety envelope**

- Each branch is capped at 5 rounds. If it cannot resolve within 5
  rounds, the question is escalated to the user for scope
  refinement rather than continuing silently.
- Each round commits and pushes. User `stop` command respected
  immediately (no ScheduleWakeup fired if user intervenes).
- Destructive git operations (delete, force-push, reset) remain
  forbidden without explicit user authorisation.
- K-Dense Web prompts are staged in `branches/*/k_dense_prompt.md`
  so the user can launch them manually.

**Cross-branch coordination**

- Each branch reads the others' synthesis documents before its own
  final round, to check that recommendations do not conflict.
- A final integration round (R9 in main loop, post-branches)
  consolidates branch outputs into a single experimental-protocol
  recommendation document.

## Branch roster

- [`B_Q09_serial_dependence/`](B_Q09_serial_dependence/) — first
  kick-off (design-decision urgency).
- [`B_Q05_hmc_power/`](B_Q05_hmc_power/) — second (experiment
  feasibility).
- [`B_Q06_time_varying_prior/`](B_Q06_time_varying_prior/) — third
  (α_sda decontamination).
