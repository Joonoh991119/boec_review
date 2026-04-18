# R7 Synthesis

---

## Ganguli — α-axis does not subsume BEC or PPC (L19)

**Decision**: **ACCEPT**. The α-axis reframing (R1) parameterises
hypotheses *within* the Wei-Stocker MI-maximising meta-framework. It
does NOT index Bayesian Efficient Coding (Park-Pillow 2024) or
probabilistic population codes (Ma et al. 2006). Each of these is a
distinct meta-framework with its own optimal encodings.

**Simulator amendment**: add new §"Meta-framework commitment" block
before §Models we did not fit. Content:

> The simulator commits to Wei-Stocker-style static-tuning
> efficient coding with mutual-information-maximising objective.
> The α-axis from §The η-axis and its Prat-Carrabin-Woodford
> framing parameterises hypotheses *within* this meta-framework;
> it does NOT index alternative meta-frameworks. Distinct
> meta-theoretical commitments exist and are not covered here:
>
> - **Bayesian Efficient Coding** (Park & Pillow 2024) replaces
>   MI-maximisation with a user-specified Bayesian loss; different
>   encoding losses yield different optimal tuning curves.
> - **Probabilistic Population Codes** (Ma, Beck, Latham & Pouget
>   2006; Beck et al. 2011; Pouget et al. 2013; Walker et al.
>   2020) represent uncertainty in the population-activity
>   shape, not a scalar m. The m-space collapse in Bundle B (i)
>   absorbs this into Gaussian noise.
>
> HMC conclusions here read as "favouring α-value X *within* the
> Wei-Stocker BOEC meta-framework", not as "rejecting BEC or PPC."

---

## Fool — dynamical and resource-rational alternatives (L21)

**Decision**: **ACCEPT**. Prat-Carrabin, Harl & Gershman 2026
gain-adaptive recurrent networks produce "adapter repulsion" that
mimics BOEC repulsion under the mirror-skew design. Resource-rational
(Lieder-Griffiths 2020; Bhui-Lai-Gershman 2021) adds another
unfitted family.

**Simulator amendment**: extend §Models we did not fit with two new
bullets:

> **4. Gain-adaptive recurrent networks** (Prat-Carrabin, Harl &
>    Gershman 2026). Dynamical efficient coding where tuning
>    curves adapt to recent stimulus history. Under narrowly-peaked
>    priors the optimal gain configuration yields "adapter
>    repulsion" that is behaviourally indistinguishable from BOEC
>    repulsion at trial-averaged bias. Related: Gonzalo Cogno et
>    al. 2023; Barrett et al. 2021.
> **5. Resource-rational / rational inattention** (Lieder &
>    Griffiths 2020 BBS; Bhui, Lai & Gershman 2021; Woodford 2020).
>    Observer uses bounded computation; biases depend on ITI,
>    cognitive load, and response deadline — variables the current
>    design does not vary.

Also extend §Parametric commitments with a new line:

> **Static tuning curves (no gain adaptation across trials)** —
>   Wei-Stocker framework assumption. Violated under PCHG 2026
>   gain-adaptive recurrent networks. Adapter-repulsion mimics
>   BOEC repulsion; distinguishing requires trial-history
>   variables not in the current design.

---

## Hahn — meta-framework commitment is a Stage-1a item (L21)

**Decision**: **ACCEPT**. Meta-framework commitment is a
pre-registration disclosure not previously listed.

**Simulator amendment**: append to §Registered-report readiness
and gaps (R6) a paragraph:

> "A ninth registered-report disclosure is the
> **meta-framework commitment**: this simulator commits to
> Wei-Stocker-style static-MI efficient coding. Alternative
> meta-frameworks (BEC, PPC, gain-adaptive recurrent networks,
> resource-rational) are NOT tested. A registered report using
> this simulator's H-set can only claim to discriminate *within
> the Wei-Stocker meta-framework*, not between meta-frameworks.
> The ninth disclosure makes this explicit."

---

## Summary of R7 amendments

### Accepted (applied to boec_simulator parallel commit)

1. New §Meta-framework commitment block (before §Models we did
   not fit). States Wei-Stocker-static-MI commitment and lists
   BEC + PPC as uncovered alternatives.
2. §Models we did not fit extended with gain-adaptive recurrent
   networks (PCHG 2026) and resource-rational bullet.
3. §Parametric commitments extended with "Static tuning curves (no
   gain adaptation)" bullet.
4. §Registered-report readiness and gaps extended with ninth
   disclosure (meta-framework commitment).

### Retired lenses

- L19, L21 move to Completed. With R7 closed, all 22 enumerated
  lenses (including mid-loop additions L16-L22) are retired.

### Widening citations

16 non-anchor refs engaged (Park-Pillow 2024, Ma-Beck-Latham-Pouget
2006, Beck-Latham-Pouget 2011, Pouget-Beck-Ma-Latham 2013,
Walker-Cotton-Ma-Tolias 2020, Polanía-Woodford-Ruff 2019,
Prat-Carrabin-Harl-Gershman 2026, Gonzalo Cogno et al. 2023,
Barrett et al. 2021, Ali et al. 2023, Lieder-Griffiths 2020,
Bhui-Lai-Gershman 2021, Icard 2024, Mandelbaum et al. BBS
commentary, Woodford 2020, Prat-Carrabin-Woodford 2020).
Cumulative R1-R7: ≈ 100 non-anchor references.

### Next round (R8) — status

All primary + integration lenses retired. R8 should be a
**consolidation / synthesis round**: produce a compact outward-
facing summary (README for boec_review itself + a §Executive
summary for the simulator) that a lab external reader can use
without walking the 7-round audit trail. R8 is also the natural
checkpoint to ask the user whether to continue with further lenses
(e.g., a targeted revisit of any deferred open question) or to
pause the loop.
