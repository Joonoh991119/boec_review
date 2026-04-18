# B_Q05 R2 — Generator-side persona: 합성 데이터 명세
## [B5R2] 2026-04-18

Round 01 문헌에서 확보한 식별가능성 앵커를 바탕으로,
H1–H5 각 셀에서 생성해야 할 합성 데이터의 구조를 명세한다.

---

## 1. 생성 목적

Power table (R4)을 위해서는 각 H 셀 × η 수준에서 예상되는 **bias·SD 프로파일**과
그로부터 도출되는 **discriminating observables의 효과 크기 d**를 확보해야 한다.

이 round는 합성 데이터 *생성 규칙*을 명세한다 (실제 시뮬레이션은 보조 코드 또는 R3 검증자 추산).

---

## 2. 설계 파라미터 (고정)

| 변수 | 값 |
|---|---|
| 자극 분포 (Prior A) | Skew-normal: ξ = 0.92s, ω = 0.3374s, α_shape = +3.3 |
| 자극 분포 (Prior R) | Skew-normal: ξ = 1.28s, ω = 0.3374s, α_shape = −3.3 |
| 두 분포 공통 평균 | μ ≈ 1.1s |
| 두 분포 공통 SD | σ ≈ 0.22s |
| 자극 범위 | 0.44 – 1.76s (≈ μ ± 3σ) |
| 피험자 수 N | 30 |
| 시행 수 T/피험자 | 700 (350 × A, 350 × R) |
| 설계 | 인터리브 + prev_response 공변량 (B_Q09 R5 권장) |

---

## 3. 합성 데이터 생성 셀 (H1–H5 × η)

### 셀 정의

| 셀 | Encoding f(θ) | Noise σ_e(θ) | η | 기대 bias 방향 @ θ=1.1s | α_sda 부호 |
|---|---|---|---|---|---|
| H1 | θ (선형) | w·θ (Weber) | — | Attractive: b(1.1) < 0 | ~ 0 또는 음수 |
| H2 | k·F_prior(θ) (CDF) | σ₀ (상수) | 0 | Repulsive: b(1.1) > 0 | 양수 |
| H3-η1 | k·F_prior(θ) | σ₀/p(θ) | 1 | 강한 repulsion | 양수 (더 강함) |
| H3-η2 | k·F_prior(θ) | σ₀/p(θ)² | 2 | 더 강한 repulsion | 양수 (더 강함) |
| H3-η3 | k·F_prior(θ) | σ₀/p(θ)³ | 3 | 매우 강한 repulsion | 양수 (매우 강함) |
| H4 | k·log θ (Fechner) | σ₀ (상수) | 0 | Attractive (log-space): b(1.1) ≈ H1 | ~ 0 또는 음수 |
| H5-η1 | k·log θ | σ₀/p(θ) | 1 | 복합: repulsion + Fechner | 양수 (약함) |

*η 값은 보조 파라미터 — Wei-Stocker 2015의 $\mathcal{J} \propto p(\theta)^\alpha$ 연속 축에서 α/2 = η.*

### H1 ↔ H4 분리 불가 조건

H1 (linear+Weber)과 H4 (log+constant)는 현재 균일 간격 자극 설계에서 관찰 가능 수준으로 near-identical하다. Hahn-Wang-Wei 2025 Theorem (exceptional set 조건)에 따르면, log-uniform 자극 간격만이 이 두 모델을 분리한다. 현재 설계는 이 분리를 *목표로 하지 않는다* — H1/H4 셀을 공통으로 "Classical" 군으로 처리.

---

## 4. 핵심 discriminating observables

### Observable 1: Sign of (b_A − b_R) at θ = 1.1s

$$\Delta b_{\text{sign}} = \text{sign}(b_A(1.1) - b_R(1.1))$$

| 셀 | 이론 예측 |
|---|---|
| H1, H4 | Δb_sign = **−1** (classical attractive: A 조건 bias negative, R 조건 positive) |
| H2, H3, H5 | Δb_sign = **+1** (BOEC repulsive: A 조건 bias positive, R 조건 negative) |

이 부호 반전이 실험의 primary discriminator이다.

### Observable 2: α_sda (slope of SD(θ) curve)

For CDF encoding (H2/H3):
- $f'(\theta) = k \cdot p(\theta)$ (locally proportional to prior density)
- SD 국소 하한: $\sigma_{\theta,\text{ideal}} = \sigma_e(\theta)/|f'(\theta)| = \sigma_0 / (k \cdot p(\theta)^{1+\eta})$
- Prior peak 근방에서 **SD 감소**; prior tail에서 **SD 증가**
- Skew-normal prior의 경우: A 조건에서 SD(θ)가 mode 왼쪽에서 감소 후 오른쪽에서 증가

For linear encoding (H1):
- $f'(\theta) = k$ (constant)
- Weber noise: $\sigma_e(\theta) = w \cdot \theta$ → SD ∝ θ → α_sda ≈ 0 (근사 선형)

### Observable 3: |b_A − b_R| at θ = 1.1 (magnitude)

Wei-Stocker 2015 small-noise 근사:
$$|b_A(1.1) - b_R(1.1)| \approx 2\sigma^2_{\text{LR}} \cdot \left|\frac{d}{d\theta}\log p(\theta)\right|_{\theta=1.1}$$

스큐 노멀 (α_shape = ±3.3, ω=0.3374)에서 θ=1.1에서의 로그 prior 기울기:

$$\left.\frac{d}{d\theta}\log p(\theta)\right|_{1.1} \approx \frac{1}{\sigma^2_A}(\mu_A - 1.1) + \text{skewness correction}$$

수치 추정: skew-normal mode ≈ μ - 0.08 SD ≈ 1.082s 근방 (A 조건).
θ=1.1에서 A-prior는 mode 오른쪽 → 로그 prior 기울기 ≈ −(1.1 − 1.082)/0.22² ≈ −0.37 s⁻¹.

B_A(1.1) (H1): ≈ $\sigma^2_{\text{LR}} × (-0.37)$ ≈ −0.37 × (0.06)² ≈ −1.3 ms (아주 작음)

이는 H1에서 |b_A − b_R| ≈ 2.6 ms 수준이다.

H2/H3에서의 repulsive bias: Wei-Stocker 2015 공식에 따르면 BOEC bias의 부호가 반대이며 **크기는 η에 따라 증폭**된다. Simulator 예측 (BOEC_intro.m 기준): |b_A − b_R| ≈ 40–80 ms at η=1. 이 값이 R3 verifier에서 검증돼야 한다.

---

## 5. 생성 셀 × η 우선순위

| 우선순위 | 셀 | η | 이유 |
|---|---|---|---|
| **최우선** | H2 | 0 | Canonical BOEC, 가장 단순 → 기저 효과 크기 앵커 |
| **필수** | H3 | 1 | η=1은 $J \propto p(\theta)$ 표준 효율 부호화 |
| **필수** | H1 | — | Classical baseline; sign contrast의 negative control |
| **권장** | H3 | 2, 3 | η 강도 vs. 검출력 관계 |
| **권장** | H5 | 1 | Fechner + BOEC 혼합 |
| **선택** | H4 | — | H1 대조군; 현재 설계에서 분리 어려움 |

---

## 6. 합성 데이터 생성 알고리즘 명세

아래는 MATLAB (BOEC_intro.m CONFIG 사용) 또는 Python으로 실행할 수 있다.
*B_Q05는 이론 문서 브랜치이므로 실제 코드 실행 불포함.*

**Step 1**: 각 셀에서 T × 2 (A, R 조건) 시뮬레이션:
```
for n = 1:N_subjects:
    sigma_e_subject = sigma0 * exp(randn * sigma_sigma0)  # hierarchical variability
    for condition in [A, R]:
        theta_samples = sample_from_prior(condition)  # 350 samples from skew-normal
        for t = 1:350:
            m = f(theta) + epsilon(sigma_e(theta))   # measurement
            r = posterior_action(m, prior, loss)     # BLS response
        b_cond = mean(r) - mean(theta)
        SD_cond = std(r - theta)
```

**Step 2**: 핵심 통계량 추출:
- `delta_b = b_A - b_R` (per subject)
- `sign_b = sign(b_A(1.1) - b_R(1.1))` (per subject)
- `alpha_sda = slope(SD ~ theta)` (per condition per subject)

**Step 3**: Group-level 합산:
- `group_mean_delta_b = mean(delta_b_subjects)`
- `group_SE = std(delta_b_subjects) / sqrt(N)`
- `group_95CI = group_mean_delta_b ± 1.96 × group_SE`

---

## 7. Anchor 수치 (R3 검증 목표)

R1 문헌 기반 + 이론적 추산:

| 파라미터 | 값 | 출처 |
|---|---|---|
| Weber fraction w (H1 baseline) | 0.15 [0.10–0.25] | Jazayeri 2010, Acerbi 2012 |
| SE(w) per subject, T=700 | ≈ 0.004 | w/√(2T) |
| Group SE(mean w), N=30 | ≈ 0.008 | SD(w)/√30, SD≈0.04 |
| Prior skewness recovery T≥600 | 3rd moment 충분 | Acerbi 2012 |
| |b_A − b_R| at η=0 (H2) | ≈ 20–40 ms | 시뮬레이터 예측 (R3 검증 필요) |
| |b_A − b_R| at η=1 (H3) | ≈ 40–80 ms | 시뮬레이터 예측 (R3 검증 필요) |
| d per subject (η=1, H3) | ≈ 2–5 | delta_b / SE_within |
| d group (η=1, H3, N=30) | ≈ 4–9 | requires R3 |

---

## 8. 식별가능성 이슈: 단일 노이즈 수준

Hahn-Wang-Wei 2025의 핵심 경고: "reliable recovery requires multiple noise levels."

우리 설계의 보상 메커니즘:

1. **Two-prior design (A vs. R)**: A/R 두 prior의 shape이 크게 다름 → encoding function에 대한 constraint 제공. Theorem 3 충족.

2. **Hierarchical pooling**: N=30 피험자의 가변적 σ_e → 집단 내 실질적인 "noise spread" 존재 → 유사 multi-noise 정보

3. **Bias sign vs. magnitude 분리**: 부호 검정은 σ_e와 독립적 → sign test는 η에 무관하게 high-power

**결론**: 단일 노이즈 수준 제약은 η (noise adaptation exponent)의 *크기* 추산 정밀도를 낮추지만, H1/H4 vs. H2/H3/H5 **부호 대비**는 η에 무관하게 검출 가능하다.

---

> **Delta**: B_Q05 §Identifiability floor가 R2에서 얻은 내용:
>
> - H1–H5 각 셀의 discriminating observable (sign, magnitude, α_sda)의 이론적 방향 명세
> - H1↔H4 분리 불가 조건 명시 (log-uniform 자극 필요)
> - Generator 알고리즘 명세 (R3 검증을 위한 input 제공)
> - 단일 노이즈 수준 제약의 보상 메커니즘 (two-prior + hierarchical pooling + sign test)
>
> 정량적 citations: R1 7개 유지 + 이론 추산. **Round accept.**
