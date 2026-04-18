# MIGRATION — autoresearch expansion

**Purpose.** This document migrates the theoretical-review loop to a
Karpathy-style `autoresearch` regime for the next session. It is
self-contained: a fresh session can read this file plus
`rounds/R08_executive_summary.md` and resume the loop without
walking R1–R7.

---

## 1. Research context (carry-forward for any autoresearch agent)

### 1.1 The question

A duration-reproduction psychophysics experiment uses two
skew-normal priors of opposite skewness (A right-skew, R left-skew,
matched mean $\approx 1.1$ s, SD $\approx 0.22$ s, shape parameter
$\alpha = \pm 3.3$, scale $\omega = 0.3374$). For every subject, the
experiment asks:

- **Behavioural**: does the subject learn the imposed prior, and
  does their $\mathrm{bias}(\theta) / \mathrm{SD}(\theta)$ signature
  flip with the prior's skew sign?
- **Parameter-recovery**: can an individual's encoding noise
  $\sigma_e$ and subjective prior $p^{\mathrm{subj}}_{\mathrm{prior}}$
  be recovered by hierarchical HMC fitting a Bayesian observer
  model?

### 1.2 Working hypotheses

Five cells on the encoding × noise plane, with loss closed to BLS
($L^2$) and subjective = objective for identifiability:

| Cell | Encoding $f(\theta)$ | Noise $\sigma_e(\theta)$ | Family |
|---|---|---|---|
| H1 | $\theta$ (linear) | $w \cdot \theta$ (Weber) | classical attractive |
| H2 | $k \cdot F_{\mathrm{prior}}(\theta)$ | $\sigma_0$ | canonical BOEC |
| H3 | $k \cdot F_{\mathrm{prior}}(\theta)$ | $\sigma_0 / p(\theta)^\eta$ | strong BOEC |
| H4 | $k \cdot \log \theta$ (Fechner) | $\sigma_0$ | classical log |
| H5 | $k \cdot \log \theta$ | $\sigma_0 / p(\theta)^\eta$ | modular BOEC |

H2 / H3 / H5 are sample points on a continuous
$\mathcal{J} \propto p(\theta)^{\alpha}$ axis
(Prat-Carrabin-Woodford 2020). H1 and H4 are observationally
near-equivalent within the current design — separation requires
log-uniform stimulus spacing (Hahn-Wang-Wei 2025 exceptional set).

### 1.3 Inductive biases (to be kept visible)

Any autoresearch agent working on this project inherits these
biases; the agent must not hide them.

- **Wei-Stocker meta-framework commitment** — static-tuning efficient
  coding with MI-maximising objective. Alternative meta-frameworks
  (BEC, PPC, gain-adaptive recurrent, resource-rational, rational
  inattention) are NOT tested.
- **8-anchor paper bias** — Stocker-Simoncelli 2006, Jazayeri-Shadlen
  2010, Acerbi 2012, Wei-Stocker 2015, Wei-Stocker 2016, Hahn-Wei
  2022/2024, Hahn-Wang-Wei 2025, Prat-Carrabin-Gershman 2025.
  Replication status is non-uniform (classical anchors robust;
  recent anchors < 2 years unreplicated; see simulator README
  §Anchor-paper replication status).
- **Parametric commitments** (nine items) — skew-normal mirror
  priors, subjective = objective, stationary prior, BLS $L^2$,
  Gaussian additive m-noise, no motor noise, no lapse rate, iid
  trials, additive-$\delta$ on $f(\theta)$, static tuning curves.
  Bundle B in the simulator README consolidates the eight
  auxiliaries.
- **Observable-choice bias** — primary discriminators (bias sign
  at $\theta = 1.1$, $\alpha_{\mathrm{sda}}$) maximise separability
  *within* H1–H5; a fresh researcher blind to the family might
  prefer response skewness, bias at prior modes, or minimum-SD
  location (see R1 L03 and R7 L19).

### 1.4 What R1–R8 changed (consolidated)

The simulator now carries: §Parametric commitments, §Design axes
and closures (with veridical + stationarity caveats), §Working
hypotheses with empirical-precedent caveat, §The η-axis and its
Prat-Carrabin-Woodford framing (α-axis), §Auxiliary-assumption
bundle (Bundle B), §Models we did not fit (six frameworks), §Meta-
framework commitment, §Identifiability floor, §Interpretive scalars
(Q(θ) with Z > 2 falsifier), §Anchor-paper replication status,
§Registered-report readiness and gaps (nine disclosures).

Full round-by-round detail in `rounds/R01_synthesis.md` through
`rounds/R08_executive_summary.md`.

---

## 2. Current state: three open branches

Three mini-loops are seeded but not yet executed. Each has a
`program.md` (Karpathy-style sufficient-condition sheet) and a
`README.md` (scope + round plan + harness pattern).

| Branch | Question | Harness pattern | Status |
|---|---|---|---|
| `B_Q09_serial_dependence/` | Interleaved vs. blocked A/R design under serial dependence | fan-out / fan-in | Phase A complete; kick-off queued |
| `B_Q05_hmc_power/` | Hierarchical HMC posterior widths at realistic N × T | generate-and-verify | Phase A complete; queued |
| `B_Q06_time_varying_prior/` | Decomposition of α_sda into learning-driven vs. encoding-driven | pipeline | Phase A complete; queued |

---

## 3. Karpathy autoresearch protocol adapted

(See [karpathy/autoresearch](https://github.com/karpathy/autoresearch),
released 2026-03.) The ML-experiment loop (propose → train → evaluate
→ keep-if-improved → repeat) maps to our theoretical review as:

| Karpathy element | Our adaptation |
|---|---|
| `program.md` methodology sheet | `branches/*/program.md` (Objective / Modify / Leave-alone / Evaluation / Failure-handling / No-help / Budget / Delta) |
| propose (modify train.py) | external-research pass + persona critique |
| train (5-minute run) | synthesis document drafting |
| evaluate (validation loss) | Delta-check: did the simulator gain quantitative content? |
| keep-if-improved | simulator README amendment only on accept |
| budget (2-day wall) | 5-round cap per branch; early-exit on non-improvement |
| "never ask for help" | autonomous within branch; escalate only on failure-handling boundary |

**Hybrids kept for our use case**:
- Unlike Karpathy, we *do* carry cross-round memory within a branch
  (earlier rounds inform later ones).
- Unlike Karpathy, we *do* cross-reference between branches at
  Round 4 to avoid contradictory recommendations.

---

## 4. Resume instructions for next session

The session ends here by user directive. A fresh session should:

1. Read `rounds/R08_executive_summary.md` (600-word state).
2. Read this file.
3. Read the three `branches/*/program.md` sheets.
4. Kick off **B_Q09_serial_dependence R1** first (design-decision
   urgency). Use fan-out pattern: three parallel Zotero + WebSearch
   passes on sensory carryover, decisional carryover, motor-response
   coupling. Record to `branches/B_Q09_serial_dependence/round01_findings.md`.
5. After B9R3 synthesis lands, kick off B_Q05 R1 (or in parallel if
   user allows).
6. Cycle through each branch to its completion or early-exit.
7. Final integration: write `rounds/R09_branch_integration.md`
   consolidating the three branches' final recommendations into a
   single §Experimental-protocol recommendation block for the
   simulator.

**Tools to use each round**:
- Zotero MCP (`mcp__zotero__*`) — semantic search, fulltext,
  abstract retrieval.
- WebSearch — recent-literature + critique verification.
- K-Dense Web prompts staged in each branch's `k_dense_prompt.md`;
  agent reads `k_dense_response.md` if user has pasted one, else
  notes absence and proceeds.
- Local skills (at `skills-repo/claude-scientific-skills/scientific-skills/`):
  `literature-review`, `peer-review`, `scientific-writing`.
- Harness patterns from `skills-repo/harness/skills/harness/SKILL.md`.

**Safety envelope (binding)**:
- No destructive git (force-push, reset, delete of tracked files).
- User `stop` command halts all ScheduleWakeup chains.
- 5-round cap per branch; escalation to user at failure-handling
  boundaries rather than silent continuation.
- Amend/force-push forbidden without explicit user authorisation.

**Commit-message prefix conventions**:
- `[BxxRn]` for branch rounds in `boec_review`.
- `[boec_simulator ← boec_review BxxRn]` for cross-ref amendments.
- Main-loop rounds: `[Rn]`.
- Consolidation / integration: `[Rn-consolidation]` or
  `[R9-integration]`.

---

## 5. Open questions (Q01–Q09) and gate conditions

For full registration (Stage 1b registered report), the following
questions must be resolved:

- **Q05** — Hierarchical-HMC power analysis (⇦ B_Q05 covers this).
- **Q06** — Time-varying-prior HMC (⇦ B_Q06 covers this).
- **Q09** — Serial-dependence simulation (⇦ B_Q09 covers this).
- Q07 — $(\alpha, \omega)$ sensitivity sweep (design already
  committed; lower priority).

Q01 (continuous α-axis re-parameterisation), Q02 (subject-conditional
bands), Q03 (decoupled encoding/decoding priors), Q04 (Q(θ) null
distribution), Q08 (response-skewness auxiliary threshold) remain
deferred as simulator-code or pilot-data tasks not addressed by
theoretical review.

---

## 6. What the next session should avoid

- Re-opening retired lenses (L04–L22) without new evidence.
- Running external research on topics already deeply cited in R1–R8
  (anchor-paper overfit; R3 L11/L12/L13 already broke out of the
  Wei-Stocker echo chamber).
- Escalating simulator code edits without explicit user authorisation
  (these are Q01 / Q06 / Q09 simulator-code tasks, not theoretical
  review tasks).
- Extending the main loop with further lenses; R8 concluded the
  enumerated backlog. New lenses require user authorisation.

---

*End of migration. The next session can use this file to resume the
autoresearch regime on the three branches without walking the full
R1–R8 audit trail.*
