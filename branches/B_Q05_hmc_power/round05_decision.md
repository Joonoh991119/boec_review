# B_Q05 R5 — 결정: 현재 설계의 검출력 충분성
## [B5R5] 2026-04-18

---

## 1. 결정 요약

**현재 설계 (N=30, T=700): 충분히 검출력 확보됨.**

R1–R4의 분석을 종합:

| 검정 | 검출력 | 결론 |
|---|---|---|
| H1/H4 vs. H2/H3 sign contrast | >99.9% | 과잉 검출력 |
| H2 vs. H3 magnitude 구별 | >91% | 충분 |
| Prior 3차 모멘트 회복 | >99% | 충분 |
| Per-subject η 추산 | CI ±0.5 | 부분 불확실 (단일 노이즈) |
| 종합 판정 | **ADEQUATE** | — |

---

## 2. Simulator amendment 제안

Bundle §Identifiability guarantees and sample-size floor에 추가할 단락:

```
## Sample-size floor (B_Q05 review, 2026-04-18)

At the current design (N = 30 subjects × T = 700 trials, two
mirror-skew priors A/R, single sensory-noise level per subject,
interleaved + prev_response covariate), hierarchical HMC analysis
is expected to provide:

(i) Group-mean Weber fraction 95% CI width: ±0.014 (total 0.028;
    ~19% relative at w ≈ 0.15). Anchored by Jazayeri-Shadlen 2010
    per-subject range and Acerbi 2012 noise characterisation.

(ii) Group-mean sign contrast (b_A − b_R) 95% CI width: ±9 ms
    (N = 30, between-subject SD ≈ 25 ms). Effect-size d ≥ 4.4
    (H2 baseline) to d ≥ 8.7 (H3-η1 baseline) — power >99.9%.
    This is the primary H1/H4 vs. H2/H3/H5 discriminator.

(iii) Per-subject σ_e 95% CI width: ±4 ms (CRLB × 1.2 overhead
    at T = 700). Single noise level limits separation of σ₀ from η;
    hierarchical partial pooling provides partial compensation
    (HWW 2025 Theorem 3 two-prior partial transfer).

(iv) Per-subject subjective-prior shape: 1st–3rd moment recoverable
    at T ≥ 600 (Acerbi 2012). 4th moment (kurtosis) biased; but
    our skew-normal prior is characterised by 3rd-moment skewness
    (α_shape) which IS recoverable.

Sample-size floor: N ≥ 10 achieves >99.9% power for the primary
sign-contrast discriminator (d ≥ 5 at H3-η1). N = 30 provides
overdetermined evidence for group-level BOEC vs. classical
discrimination. Additional subjects improve η-estimation precision
(CI ±0.5 per subject → ±0.1 group with N = 30) but are not
required for binary H-cell classification.

Critical caveat: Power estimates assume |b_A − b_R| ≥ 10 ms
(simulator-predicted range 40–80 ms at H3-η1). If pilot data
shows |b_A − b_R| < 10 ms, N ≥ 65 would be required for 80%
power. The falsifiable threshold from B_Q09 (pilot |b_A − b_R|
≥ 43 ms) serves as the gate condition. [B5R5 amendment]
```

---

## 3. 추가 피험자/시행 기준

만약 파일럿 데이터가 |b_A − b_R| < 10ms를 보인다면:

| 피험자 추가 목표 | 필요 N (80% power) |
|---|---|
| |b_A−b_R| = 20ms | N ≥ 15 |
| |b_A−b_R| = 10ms | N ≥ 65 |
| |b_A−b_R| = 5ms | N ≥ 250 |

시행 수 T를 늘리는 것은 signal-to-noise 비율보다 within-subject precision에 영향을 주며, group-level CI 폭에는 N을 늘리는 것이 더 효과적이다.

---

## 4. 브랜치 수렴 판정

program.md accept 기준:
- ✓ Power table with ≥2 literature-anchored effect-size estimates (7개 citations, 2 anchors: Jazayeri 2010 + Acerbi 2012)
- ✓ 95% CI widths traceable derivation (CRLB × 1.2, HWW 2025 partial transfer)
- ✓ Delta-check: simulator §Identifiability 신규 내용

**B_Q05 브랜치 CLOSED. → B_Q06 R1 착수.**

---

> **Delta**: B_Q05 §Identifiability guarantees and sample-size floor 최종 내용:
>
> - Power table 완성: d ≥ 4.4 (H2) to d ≥ 8.7 (H3) → 검출력 >99.9%
> - N=30 sample-size floor 정당화: binary H-cell 분류에 과잉 검출력
> - 파일럿 gate 조건: |b_A−b_R| ≥ 10ms (N=30 기준) or ≥43ms (B_Q09 threshold)
> - Single noise level 제약: η CI ±0.5 (per-subj), ±0.1 (group-level with N=30)
>
> 정량적 citations: 7개. **Round accept. 브랜치 종료.**
