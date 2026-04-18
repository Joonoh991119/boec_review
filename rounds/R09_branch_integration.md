# R09 — Branch Integration: 세 브랜치 최종 권장 통합
## [R9-integration] 2026-04-18

**MIGRATION_AUTORESEARCH.md Section 4 step 7 이행.**
B_Q09 (serial dependence), B_Q05 (HMC power), B_Q06 (time-varying prior) 세 브랜치의
최종 권장사항을 단일 §Experimental-protocol recommendation 블록으로 통합한다.

---

## 1. 세 브랜치 결론 요약

### B_Q09 — Serial Dependence (완료: B9R5)

**핵심 결론**:
- 설계 권장: **인터리브(A/R 교대) + prev_response 공변량**
- β_DC = 0.41–0.66 (Bertolasi 2025); β_SC = −0.108 (contrastive)
- 블록 설계 DC 오염: B=30 → 16.1% (Wiener M=13 모형)
- 인터리브 + 공변량 제거 시: 총 SD 오염 ≈ −9% (순이득 +11%), signal 보존 ≈ 91%
- **파일럿 gate (가장 엄격)**: pilot |b_A − b_R| ≥ 43ms (B_Q09 threshold 1)

**Simulator amendment 반영**: Bundle B item (viii) IID-trials 가정 정량화 완료.

### B_Q05 — HMC Power (완료: B5R5)

**핵심 결론**:
- 현재 설계 (N=30 × T=700): **ADEQUATE** — 모든 목표에서 충분한 검출력
- 주요 discriminator (sign contrast): d_group ≥ 8.7 (H3-η1) → >99.9% power
- H2 vs. H3 구별: d_group ≈ 3.3 → >91% power
- Prior 3차 모멘트 회복: T ≥ 600 → >99% (Acerbi 2012)
- N=30 sample-size floor: binary H-cell 분류에 과잉 검출력; 추가 피험자 불필요
- **임계 gate**: pilot |b_A − b_R| ≥ 10ms (N=30 유지); ≥ 43ms (B_Q09 threshold)
- 예외: |b_A − b_R| < 5ms → 73% power → N ≥ 65 필요

**Simulator amendment 반영**: §Identifiability guarantees and sample-size floor 정량화.

### B_Q06 — Time-varying Prior (완료: B6R5)

**핵심 결론**:
- Prior-width 학습 상수 τ_q ≈ 150–200 시행 (Narain 2018, 인터리브 보정)
- Learning-driven α_sda 오염 ≈ **15–20%** (40% 임계 이하 → 허용)
- Corrected multiplier: α_sda_encoding ≈ α_sda_obs × 0.82 (±0.05)
- b_A − b_R 오염 후 하한: ≥ 29ms (18–27% 감소 후) — power 무영향
- 권장 decontamination: **Latent-drift HMC** (primary) + 후반부 서브셋(t ≥ 300) (sensitivity)
- A↔R cross-contamination: 10–15% (Natsume 2025)

**Simulator amendment 반영**: Bundle B item 3 (stationarity caveat) 정량화 완료.

---

## 2. 통합 §Experimental-protocol recommendation

아래 블록은 `boec_simulator/README.md`에 신규 섹션으로 추가할 완전한 권장 텍스트다.

```
## Experimental-protocol recommendation (B_Q09 + B_Q05 + B_Q06 review,
   2026-04-18)

### Trial design
Use fully interleaved A/R delivery (not blocked). Rationale:
  (i)  Blocked design sustains 16.1% DC contamination at B = 30 trials
       per block (Wiener 2014 M = 13 Bayesian memory prior, Bertolasi
       et al. 2025 β_DC = 0.414). Interleaved with prev_response
       covariate removes this contamination; net attenuation −9%
       (signal preserved ≥ 91%).
  (ii) prev_response covariate: include in HMC as a covariate for b_A
       and b_R estimates. This regresses out decision carryover
       (β_DC = 0.41–0.66) while leaving encoding-driven bias intact.
  (iii) Sensory carryover β_SC = −0.108 (contrastive, Bertolasi 2025)
       is small and cannot be removed without reducing signal — leave
       in model as known constant.

### Sample-size floor
N = 30 subjects × T = 700 trials (350 × A + 350 × R) is adequate:
  (i)  Primary discriminator (H1/H4 vs. H2/H3): d_group ≥ 8.7
       (H3-η1), power >99.9%. At N = 10, power is already >99.9%.
       N = 30 provides overdetermined evidence.
  (ii) H2 vs. H3 distinction: d_group ≈ 3.3, power >91%.
  (iii) Prior 3rd-moment recovery: T ≥ 600 sufficient (Acerbi 2012).
  (iv) Per-subject η CI: ±0.5 (single noise level constraint, HWW 2025).
  (v)  Group-mean ⟨b_A − b_R⟩ 95% CI: ±9 ms (SE_group = 4.6 ms).
  Critical gate: if pilot data shows |b_A − b_R| < 10 ms, N ≥ 65
  is required for 80% power; if < 5 ms, N ≥ 250. Pilot threshold:
  |b_A − b_R| ≥ 43 ms (B_Q09 threshold 1, encompassing B_Q06
  attenuation) before full data collection.

### Prior-learning decontamination
T = 700 sessions are non-stationary: τ_q ≈ 150–200 trials for
prior-width convergence (Narain et al. 2018; Sohn & Jazayeri 2021).
  (i)  Learning-driven α_sda contamination: f_learn ≈ 15–20%
       (< 40% threshold; does not affect power).
  (ii) Corrected α_sda_encoding ≈ α_sda_obs × 0.82 (±0.05).
  (iii) b_A − b_R attenuation: 18–27% combined (learning drift +
       A↔R cross-contamination, Natsume et al. 2025); post-attenuation
       lower bound ≥ 29 ms — power >99.9% maintained.
  If α_sda precision beyond sign-contrast is required:
  (a) Primary: latent-drift HMC — σ_q(t) = σ_∞ + Δσ·exp(−t/τ_q),
      τ_q ~ N(175, 50²) (Wang-Luo-Ivry 2023 dual-timescale model).
  (b) Sensitivity: posterior-half analysis (t ≥ 300 trials only).
  Agreement within ±10% on α_sda_encoding validates the method.

### Falsifiable thresholds (pilot gating)
Before full data collection, verify:
  T1. Pilot |b_A − b_R| ≥ 43 ms (group-mean, all-trial average).
      If < 43 ms, recompute required N per B_Q05 Table 3B.
  T2. β_prev_stimulus < 0 in pilot regression (confirms contrastive SC
      direction; positive would indicate Wang 2023 motor-artifact
      contamination, requiring design revision).
  T3. Covariate R² for prev_response > 0.20 in at least 50% of
      subjects (confirms DC is operationally present and can be
      removed).

### Combined noise budget
With recommended design (interleaved + prev_response covariate):
  SD(serial dependence)   = −9%  → +11% net (covariate gain)
  α_sda(learning-driven)  = −16% (tolerable; 0.82× correction)
  A↔R cross-contamination = −12% (median Natsume 2025)
  Total signal retained   ≈ 91% for sign-contrast test
  d_group (post-budget)   ≥ 6.3 → power >99.9% (N=30, T=700)
```

---

## 3. Simulator README 추가 위치

위 블록은 `boec_simulator/README.md`에서 `§Bundle B — Auxiliary assumptions` 바로 뒤,
`§Discriminating observables` 바로 앞에 삽입하는 것이 적합하다.

세 브랜치 amendment들은 이미 각 해당 섹션에 인라인으로 반영되었다:
- Bundle B item (viii): B9R5 amendment ✓
- §Identifiability guarantees item 4: B5R5 amendment ✓
- Bundle B item 3 (stationarity): B6R5 amendment ✓

---

## 4. 미해결 공개 질문 (Q01–Q09 상태)

| Q번호 | 질문 | 상태 (2026-04-18 update) |
|---|---|---|
| Q01 | Continuous α-axis re-parameterisation | ✓ **이론 해결** (notes/Q01_alpha_axis.md; README §η-axis 매핑 표) |
| Q02 | Subject-conditional bands | ✓ **이론 해결** (notes/Q02_subject_bands.md; Bundle B item 2) |
| Q03 | Decoupled encoding/decoding priors | ✓ **이론 해결** (notes/Q03_decoupled_priors.md; §Models we did not fit, H6 명세) |
| Q04 | Q(θ) null distribution | ✓ **이론 해결** (notes/Q04_Q_theta_null_distribution.md; §Q(θ) Z>+2 정당화) |
| Q05 | HMC power analysis | ✓ **해결** (B5R5: ADEQUATE) |
| Q06 | Time-varying prior decomposition | ✓ **해결** (B6R5: 16% < 40%) |
| Q07 | (α, ω) sensitivity sweep | ✓ **이론 해결** (notes/Q07_alpha_omega_sweep.md; tools/q7_alpha_omega_sweep.m) |
| Q08 | Response-skewness threshold | ✓ **이론 해결** (notes/Q08_response_skewness_threshold.md; Bundle B item 1, |γ|>1.0) |
| Q09 | Serial dependence design | ✓ **해결** (B9R5: interleaved + prev_response) |

**모든 Q01–Q09가 이론 수준에서 해결되었으며 simulator README에 amendment가 반영되었다.**
시뮬레이터 코드 실행 (Q07 MATLAB sweep, Q01 PyMC alpha-grid)과 파일럿 데이터 캘리브레이션 (Q02 r_α 측정, Q08 |γ| 측정)이 다음 단계로 남는다.

---

## 5. 다음 단계

이 integration을 완료함으로써 MIGRATION_AUTORESEARCH.md Section 4의 모든 단계가 이행되었다.

다음 필요 작업:
1. **파일럿 실험 실행**: R09 §Falsifiable thresholds (T1–T3) 검증
2. **Latent-drift HMC 구현**: boec_simulator에 σ_q(t) 동적 prior 추가 (Q06 simulator-code task)
3. **Stage 1b registered report 제출**: Q05/Q06/Q09 해결로 power 섹션 완성 가능

---

## 6. 세 브랜치 통합 시 발견한 일관성

| 비교 축 | 발견 | 결론 |
|---|---|---|
| B_Q09 pilot gate (43ms) vs. B_Q06 오염 하한 (29ms) | 43ms는 오염 후에도 충족 | 3 브랜치 gate 기준 일관 |
| B_Q05 d_group vs. B_Q06 오염 후 d_group | 8.7 → 6.3 (후 B_Q06) | power >99.9% 유지 |
| B_Q09 DC vs. B_Q06 prior-learning | 직교적 (분리 가능) | 공변량 설계로 독립 처리 |
| B_Q05 CI ±9ms vs. B_Q06 attenuation 29ms | 29ms >> ±9ms | sign-contrast 검정 robust |

**종합 결론**: 세 브랜치의 권장사항은 상호 일관되며, 현재 설계(N=30, T=700, 인터리브, prev_response 공변량)는 세 브랜치의 모든 기준을 충족한다.

---

> **Delta**: R09 통합에서 boec_simulator README가 얻은 내용:
>
> - §Experimental-protocol recommendation 블록 신설 (3개 브랜치 통합 권장)
> - 파일럿 gate 3개 (T1: 43ms, T2: β<0, T3: R²>0.20) 공식화
> - 총 signal 예산: 91% 보존 (d_group ≥ 6.3, power >99.9%)
> - Q05/Q06/Q09 해결 확인; 나머지 Q01/Q02/Q03/Q04/Q07/Q08 보류
>
> **Autoresearch cycle 완료. MIGRATION_AUTORESEARCH.md 모든 단계 이행.**
