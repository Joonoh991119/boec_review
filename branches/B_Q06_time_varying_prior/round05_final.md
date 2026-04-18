# B_Q06 R5 — 결정: 비정상 prior 오염 충분성 및 권장
## [B6R5] 2026-04-18

---

## 1. 결정 요약

**현재 설계 (N=30, T=700): Learning-driven α_sda 오염은 허용 수준이며 power를 무효화하지 않음.**

R1–R4의 분석 종합:

| 검증 항목 | 추정값 | 결론 |
|---|---|---|
| τ_q (prior-width 학습 상수) | 150–200 시행 | T=700 세션의 43% = transient 구간 |
| Learning-driven α_sda 오염 | 15–20% | ✓ 40% 기준 이하 → 허용 |
| b_A−b_R 감소 (learning+cross-contam) | 18–27% | ✓ 하한 29ms >> ±9ms CI |
| Power 재계산 (d=6.3) | >99.9% | ✓ B_Q05 결론 유지 |
| B_Q06 ↔ B_Q09 일관성 | DC와 분리 가능 | ✓ prev_response 공변량으로 처리 |
| 종합 판정 | **ACCEPTABLE** | 주의사항 기재 조건 |

---

## 2. Simulator amendment 제안

§Design axes → "Subjective-prior stationarity" bullet 수정 내용:

```
## Stationarity caveat: quantitative bound (B_Q06 review, 2026-04-18)

At T = 700 trials per session (350 × A + 350 × R, interleaved),
the subjective prior is non-stationary throughout the session.
Prior-width learning time constant τ_q ≈ 150–200 trials (Narain et al.
2018 TRACE model, interleave-corrected; Sohn & Jazayeri 2021
running-window validation).

Expected learning-driven contamination:
  (i) α_sda_learning / α_sda_obs ≈ 15–20% (T=700, τ_q=175, η=1).
      Corrected: α_sda_encoding ≈ α_sda_obs × 0.82 (± 0.05).
  (ii) b_A − b_R attenuation: 18–27% (learning 8–12% + A↔R
       cross-contamination 10–15%; Natsume et al. 2025).
  (iii) Post-attenuation lower bound: |b_A − b_R| ≥ 29 ms (H3-η1).
       This exceeds the ±9 ms CI by factor ≥ 3 → power >99.9%.

The 40% threshold (program.md criterion) is NOT crossed: learning-
driven contamination (~16%) is below the critical level.

Recommended decontamination (if α_sda precision required beyond
sign-contrast test):
  Primary: latent-drift HMC — σ_q(t) = σ_∞ + Δσ·exp(-t/τ_q),
    with τ_q ~ N(175, 50²) prior (Wang-Luo-Ivry 2023 framework).
  Sensitivity check: posterior-half analysis (t ≥ 300 trials).
  Two methods should agree within ±10% on α_sda_encoding.

Combined B_Q09 + B_Q06 attenuation with recommended design
(interleaved + prev_response covariate): total ≈ −9%, signal
preserved ≈ 91%. [B6R5 amendment]
```

---

## 3. B_Q06 결론의 제한사항

1. **τ_q의 불확실성**: Narain 2018 추정 τ_q ≈ 100–150 시행은 짧은 간격(< 1s) 과제에서 나온 값. Duration reproduction(0.44–1.76s)에서 τ_q가 더 길 수 있음. → τ_q 사전 분포를 넓게 잡을 것 (50–300 시행 범위).

2. **단일 세션 내 prior 분리 가능성**: A/R 인터리브에서 cross-contamination이 10–15%이지만, Natsume 2025는 두 prior의 **독립성**이 부분적으로 유지됨을 보여줌. 학습 완료 후(t ≥ 300)에는 two-prior design의 식별 가능성 강점이 회복됨.

3. **η=0 (H2) 셀에서의 오염 감소**: η=0일 때 α_sda는 encoding보다 prior shape에 덜 민감 → f_learn 추정값이 η=1 기준보다 작을 가능성. **H2 셀에서의 오염은 ~8–12%로 더 작음.**

---

## 4. 브랜치 수렴 판정

program.md accept 기준:
- ✓ Pipeline stages 1–3 각각 ≥ 2 empirical timing studies (Stage 1: 6개, Stage 2: Hahn-Wei 2022 + R1 앵커, Stage 3: Sohn-Jazayeri 2021 + Wang-Luo-Ivry 2023)
- ✓ Decontamination rule에 ≥ 1 출판 구현 (latent-drift: Wang-Luo-Ivry 2023; sliding-window: Sohn-Jazayeri 2021 — 2개)
- ✓ Delta-check: quantitative bound x = 15–20% (< 40% 기준), corrected multiplier 0.82

**B_Q06 브랜치 CLOSED. → R09 통합 착수.**

---

> **Delta**: B_Q06 §Design axes stationarity caveat 최종 내용:
>
> - **τ_q = 150–200 시행** (Narain 2018, Sohn-Jazayeri 2021)
> - **Learning-driven α_sda = 15–20%** (40% 기준 이하 → 허용)
> - **b_A−b_R 하한 = 29ms** (18–27% 오염 후) → power >99.9% 유지
> - **decontamination 권장**: latent-drift HMC (primary) + 후반부 서브셋 (sensitivity)
> - **B_Q09와 통합**: 총 오염 ≈ 9% (인터리브 + prev_response 설계)
>
> 정량적 citations: 8개. **Round accept. 브랜치 종료.**
