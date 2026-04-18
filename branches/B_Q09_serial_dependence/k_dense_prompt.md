# K-Dense Web prompt — B_Q09 serial dependence

**Please launch this at [www.k-dense.ai](https://www.k-dense.ai)
when convenient.** Output goes into `k_dense_response.md` in this
directory for downstream integration.

---

## Prompt

Deep research task: serial dependence in duration reproduction
under mirror-skew priors.

For a psychophysics experiment where a subject reproduces durations
sampled from two skew-normal priors of opposite skew (A right-skew,
R left-skew, both with mean ≈ 1.1 s, SD ≈ 0.22 s, shape parameter
α ≈ ±3.3), how does trial-sequence dependency alter the subject's
predicted (bias, SD) signature?

Questions to answer:

1. **Effect-size anchors**. What is the typical magnitude of serial
   dependence (in units of % attenuation of the bias sign contrast)
   in duration-reproduction tasks under (a) condition-blocked,
   (b) condition-interleaved, and (c) random-timing
   designs?

2. **Mechanism decomposition**. How do the three main mechanisms —
   sensory carryover (Cicchini-Mikellidou-Burr 2018), decisional
   carryover (Li-Wang-Zaidel 2026 reversed effects in cross-modal
   decisions), and motor-response coupling (Wu et al. 2024) —
   interact in a mirror-skew design? Do they attenuate, cancel, or
   amplify the (b_A, b_R) sign pattern?

3. **Design recommendation**. Given the uncertainty, which design
   (interleaved A/R vs. blocked A/R vs. partially blocked with
   washouts) maximises (i) power to detect the (b_A, b_R) sign
   flip and (ii) robustness to serial-dependence contamination?

4. **Working memory delay modulation**. Bliss, Sun & D'Esposito
   (2017) find serial dependence is weak at perception but grows
   with working-memory retention. What ISI / retention-interval
   manipulations should the experiment include to quantify this?

5. **Cross-task relevance**. Cheng, Chen, Yang & Shi (2024) show
   task-type modulation (reproduction-after-reproduction vs.
   reproduction-after-bisection). If the proposed experiment uses
   only reproduction trials, what ordering controls are needed?

## Expected deliverable

- A 1000–2000 word synthesis with effect-size estimates.
- Design recommendation (interleaved vs. blocked vs. partially
  blocked) with attenuation tables.
- Bibliography of at least 15 papers, with DOIs, that the synthesis
  references.

## Reference list to seed the K-Dense query

- Wu, Y. et al. (2024). Serial dependence in time perception
  requires consistent motor responses, not shared memory alone.
  British Journal of Psychology.
- Li, Wang & Zaidel (2026). Reversed effects of prior choices in
  cross-modal temporal decisions.
- Wang, Luo, Ivry, Tsay, Pöppel & Bao (2023). A unitary mechanism
  underlies adaptation to both local and global environmental
  statistics in time perception. PLOS CompBiol.
- Cheng, Chen, Yang & Shi (2024). The impact of task measurements
  on sequential dependence: reproduction vs. discrimination.
  Psychological Research.
- Manassi, Murai & Whitney (2023). Serial dependence in visual
  perception: a meta-analysis and review.
- Cicchini, Mikellidou & Burr (2018). The functional role of serial
  dependence.
- Bliss, Sun & D'Esposito (2017). Serial dependence is absent at
  perception but increases in visual working memory.

Record the K-Dense output by pasting it (or a summary of it) into
`k_dense_response.md` in this same directory. The loop will read
from there in B9R1.
