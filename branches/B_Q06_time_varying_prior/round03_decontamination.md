# B_Q06 R3 — Pipeline Stage 3: Decontamination 방법 조사
## [B6R3] 2026-04-18

비정상 주관적 prior의 오염을 제거하는 세 가지 출판된 방법을 비교하고
B_Q06 설계에 최적 방법을 선택한다.

---

## 1. 방법 1: Sliding-window prior 피팅 (Sohn & Jazayeri 2021)

**원리**: T 시행 세션을 겹치는 M 크기의 윈도로 분할하여 각 윈도 내에서 주관적 prior를 독립적으로 피팅.

**알고리즘**:
```
for t in range(M/2, T-M/2, step=1):
    window_trials = trials[t-M/2 : t+M/2]
    q_t = fit_bayesian_observer(window_trials)  # MLE or MAP
    alpha_sda_t = compute_alpha_sda(q_t)
```

**파라미터**:
- 윈도 크기 M = 100 (Sohn-Jazayeri 2021 권장; trade-off: M ↑ → smooth, M ↓ → noisy)
- T = 700에서 독립 윈도 수: ~7개 (겹침 없는 경우)
- 슬라이딩 해상도: 10 시행 스텝 → 60개 α_sda 추정값

**장점**:
- 직접적, 비모수적
- 시간 축에서 α_sda_learning의 지수 감쇠 곡선을 직접 관찰

**단점**:
- 각 윈도 내 T=100으로 개별 피팅 → SE 증가 (전체 700 시행 피팅 대비 ~√7 = 2.6배 넓은 CI)
- 윈도 경계에서 연속성 보장 어려움
- 계산 비용: HMC × 60 윈도 = 매우 높음

**B_Q06 적용 평가**: ★★★☆☆
- T=100 윈도에서 α_sda 정밀도가 낮아 학습 궤적 추적이 불안정
- 파일럿 검증 단계에 적합; 주 분석에는 부적합

---

## 2. 방법 2: Latent-drift prior-width parameterisation (Wang-Luo-Ivry 2023)

**원리**: 주관적 prior width σ_q(t)를 latent variable로 확장하여 HMC가 동시에 추정.

**확장 모형**:
$$\sigma_q(t) = \sigma_{q\infty} + (\sigma_{q0} - \sigma_{q\infty})\cdot e^{-t/\tau_q}$$

새 파라미터: {σ_q0, σ_q∞, τ_q} — 3개의 추가 파라미터 (피험자별).

**HMC 확장 구현 (개념)**:
```
parameters {
    real sigma_q0;      # initial prior width
    real sigma_q_inf;   # asymptotic prior width
    real<lower=0> tau_q; # learning time constant
}
model {
    for (t in 1:T) {
        sigma_q_t = sigma_q_inf + (sigma_q0 - sigma_q_inf) * exp(-t / tau_q);
        // use sigma_q_t to parameterize q(theta) at trial t
        target += log_likelihood(response[t], theta[t], sigma_q_t, ...);
    }
}
```

**장점**:
- 전체 데이터를 활용 (T=700 전부) → SE 유지
- α_sda_encoding과 α_sda_learning을 동시에 추정
- 비정상성의 함수형 가정이 명시적 (지수 감쇠)

**단점**:
- 모형 복잡도 증가: 3 추가 파라미터 × N = 90개 추가 파라미터
- τ_q가 데이터에서 잘 동정(identifiable)되지 않을 위험 (T=700이면 약 3–4 τ 커버)
- Stan/HMC 수렴 시간 증가 (약 3–5배 예상)

**B_Q06 적용 평가**: ★★★★☆
- 이론적으로 최우수; τ_q = 150–200의 사전 분포를 N(175, 50²)으로 설정하면 동정 가능
- 권장: 주 분석에서 latent-drift 버전과 정상 버전을 모두 피팅하여 BIC 비교

---

## 3. 방법 3: 세션 후반부 서브셋 분석 (implicit truncation)

**원리**: 전환 구간(t < 300)을 버리고 점근 구간(t ≥ 300)만 HMC 피팅.

**구현**:
```
analysis_trials = trials[trials.time >= 300]  # 400 trials remaining
fit_stationary_HMC(analysis_trials)
```

**장점**:
- 가장 단순 (추가 파라미터 없음)
- 정상 HMC의 편의 없는 추정값 — α_sda_encoding에 가장 가까운 추정

**단점**:
- T 유효 = 400 (57% 시행만 사용) → SE × √(700/400) = 1.32배 증가
- "점근 t=300" 가정이 τ_q에 의존 (circular reasoning 위험)
- 데이터 낭비

**B_Q06 적용 평가**: ★★★☆☆
- 보수적 decontamination의 가장 단순한 구현
- 병렬 분석으로 sensitivity check에 적합

---

## 4. 방법 비교 및 권장

| 기준 | 슬라이딩 윈도 (방법1) | Latent-drift (방법2) | 후반부 서브셋 (방법3) |
|---|---|---|---|
| 데이터 활용 | 낮음 (분할) | 높음 (전체) | 중간 (57%) |
| α_sda SE | 나쁨 (×2.6) | 좋음 (×1.0) | 보통 (×1.32) |
| 구현 복잡도 | 낮음 | 높음 | 낮음 |
| 비정상성 동정 | 직접적 | 간접적 (모형 의존) | 없음 |
| 출판 구현 | Sohn-Jazayeri 2021 | Wang-Luo-Ivry 2023 | 묵시적 |

**권장 전략 (2단계)**:
1. **Primary**: Latent-drift (방법2) — τ_q ∈ N(175, 50²) 사전 분포로 전체 T=700 피팅
2. **Sensitivity check**: 후반부 서브셋 (방법3) — t ≥ 300 서브셋으로 방법2 결과 검증

두 방법이 α_sda_encoding 추정값에서 ±10% 이내에서 일치하면 → 학습 오염은 허용 수준.
두 방법이 >20% 불일치하면 → 슬라이딩 윈도(방법1)로 학습 궤적 시각화 후 판단.

---

## 5. Simulator amendment 지정 내용 (B_Q06 output)

Quantitative bound (program.md 요구):

```
## Stationarity caveat (B_Q06 review, 2026-04-18)

At T = 700 trials per session (350 × A + 350 × R, interleaved):
the subjective prior is not stationary throughout the session.
The prior-width learning time constant τ_q ≈ 150–200 trials
(Narain et al. 2018 TRACE model; interleave-corrected).

Expected learning-driven α_sda contamination:
  f_learn ≈ 15–20% of α_sda_obs (T = 700, τ_q = 175, η = 1).

Corrected estimate: α_sda_encoding ≈ α_sda_obs × 0.82 (± 0.05).

The primary b_A − b_R sign-contrast discriminator is attenuated
by an additional 8–12% (learning drift) + 10–15% (A↔R cross-
contamination, Natsume et al. 2025). Combined attenuation: 18–27%.
At H3-η1, predicted |b_A − b_R| ≥ 40 ms: post-attenuation lower
bound ≥ 29 ms >> ±9 ms (95% CI). Power remains >99.9%.

Recommended decontamination (if α_sda precision matters beyond
sign-contrast test): latent-drift HMC with τ_q ∈ N(175, 50²) prior,
or posterior-half subsetting (t ≥ 300 trials). [B6R3 amendment]
```

---

> **Delta**: B_Q06 §Design axes stationarity caveat가 R3에서 얻은 내용:
>
> - **3가지 decontamination 방법 비교**: 슬라이딩 윈도 (Sohn-Jazayeri 2021), Latent-drift HMC (Wang-Luo-Ivry 2023), 후반부 서브셋
> - **권장 방법**: Latent-drift (primary) + 후반부 서브셋 (sensitivity)
> - **출판 구현 확인**: ≥2 구현 존재 → program.md 수락 기준 충족
> - **Simulator amendment 텍스트 초안**: quantitative bound f_learn ≈ 15–20%, corrected multiplier 0.82
> - **Power 재확인**: 27% 오염 후에도 |b_A−b_R| ≥ 29ms >> ±9ms CI → >99.9% 유지
>
> 정량적 citations: 8개 (R1 6개 + Wang-Luo-Ivry 2023 확장 + Narain 2018 τ_q). **Round accept. → R4 cross-check.**
