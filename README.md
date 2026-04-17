# BOEC Review — autonomous theoretical review loop

This repository is the **theory-only companion** to
[`boec_simulator`](https://github.com/Joonoh991119/boec_simulator). It hosts
the scientific review of the ex-ante hypothesis framework for
Bayesian-observer models of duration perception — no code, no figures, no
numerical experiments. Everything here is prose, references, counter-
arguments, and decision records.

The content is produced by an **autonomous review–rebuttal co-evolution
loop**. Each round draws on three external research resources:

- **K-Dense Web** (www.k-dense.ai) — deep-research workflow for cross-
  disciplinary synthesis.
- **Web search** — real-time literature discovery and claim verification.
- **Zotero** (via MCP) — personal library of BOEC / Bayesian-observer /
  psychophysics papers, plus annotations.

The loop continues until the user halts it.

---

## Mission

Stress-test the theoretical scaffolding that
[`boec_simulator`](https://github.com/Joonoh991119/boec_simulator)
currently stands on:

- the eight anchor papers (Stocker-Simoncelli 2006, Jazayeri-Shadlen 2010,
  Acerbi 2012, Wei-Stocker 2015, Wei-Stocker 2016, Hahn-Wei 2022,
  Hahn-Wang-Wei 2025, Prat-Carrabin & Gershman 2024);
- the five working hypotheses (H1 linear × Weber, H2 eff-CDF × const,
  H3 eff-CDF × eff-prior, H4 log × const, H5 log × eff-prior) and the
  two primary discriminators ((b_R, b_L) at θ=1.1; α_sda);
- the pruning decisions that dropped four cells and closed the loss +
  subjective-prior axes;
- the claim that the mirror-skew prior design separates *prior-driven*
  from *encoding-driven* SD asymmetry.

Each round of the loop produces a Round document in `rounds/` that names
the critical lens, cites what was found in the external resources, and
concludes with either (i) a proposed amendment to the simulator README,
(ii) a new open question filed in `open_questions/`, or (iii) a claim
accepted as-is with rationale.

---

## Loop protocol

1. **Lens rotation.** Each round picks one or two lenses from the backlog
   in `open_questions/LENSES.md`. No lens repeats until all have been
   visited once.
2. **External research.** The round first performs an evidence pass
   with K-Dense Web + web search + Zotero. The raw findings go into
   `references/RN_findings.md`.
3. **Reviewer agents.** 2–3 reviewer agents read the simulator README
   and the external findings and write a critique at 300–400 words
   per agent. Critiques land in `rounds/RN_critique.md`.
4. **Synthesis and rebuttal.** A single synthesis document
   `rounds/RN_synthesis.md` answers each critique point with one of:
     - *Accept* — amend simulator README accordingly. Record the diff.
     - *Reject* — explain why, cite the counter-evidence.
     - *Defer* — file as open question and move on.
5. **Commit and push** with message prefix `[R_N]`.
6. **Schedule next wakeup** (dynamic pacing) and rotate lens.

The loop is not a replacement for peer review; it is an in-house
adversarial-collaboration protocol designed to force explicit
rationales for every methodological choice before HMC fitting begins.

---

## Directory layout

```
boec_review/
├── README.md                 # this file
├── open_questions/
│   ├── LENSES.md             # backlog of review lenses (rotating)
│   └── OPEN_QUESTIONS.md     # questions deferred from individual rounds
├── references/
│   └── RN_findings.md        # per-round external-research notes
├── reviewers/
│   └── personas.md           # standing reviewer personas
└── rounds/
    └── RN_[topic].md         # one synthesis document per round
```

---

## Rounds

| Round | Lens | Status | Commit |
|---|---|---|---|
| R0 | Loop setup | done | [R0] initial commit |
| R1 | L04 design circularity · L05 theoretical coherence · L06 H6/H7 | done | [R1] see `rounds/R01_synthesis.md` |
| R2 | L07 identifiability × sample size · L14 Q(θ) discriminator | done | [R2] see `rounds/R02_synthesis.md` |

(Future rounds appended by the loop.)

---

## Relationship to `boec_simulator`

This repo **does not** hold code or figures. If a round's synthesis
demands a simulator-level change (README amendment, new hypothesis
cell, removal of a claim), the change is applied to
`boec_simulator` via its own commit — cross-referenced from the round
document here. The two repos diverge on purpose: `boec_simulator` is
the artefact; `boec_review` is the audit trail.
