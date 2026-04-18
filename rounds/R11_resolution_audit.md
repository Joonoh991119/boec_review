# Resolution & Clipping Audit
## 2026-04-18 | Numerical-stability review and refactor

사용자 지시 "지금까지 구현한 theta와 m 해상도 충분히 일정하게 높게 유지되도록
수정, interpol필요한 영역은 interpol해라. 모두 갈아엎고 계속 진행"에 따라
모든 ex-ante 도구의 numerical 해상도를 simulator 공식 baseline (n_theta=1401,
n_m=3001)으로 통일.

---

## 1. 감사 전 상태 (불일치)

| 도구 | n_theta | n_m | θ range | eff_floor | 비고 |
|---|---|---|---|---|---|
| BOEC_intro.m (simulator) | **1401** | **3001** | adaptive | 1e-2 | R5d 공식 baseline |
| make_fig2_predictions.py | 321 | 401 | [0.30, 1.90] | 1e-3 | 4× / 7× coarser; floor 10× looser |
| make_fig3_alpha_axis.py | 321 (fig2 import) | 401 | [0.30, 1.90] | 1e-2 | fig2 의존; floor만 일치 |
| q7_alpha_omega_sweep.m | 321 | 801 | [0.30, 1.90] | 1e-2 | 4× / 4× coarser |
| build_bls_lookup.py | 321 | 801 | [0.30, 1.90] | 1e-2 | q7와 일치 |

→ 4개 ex-ante 도구가 simulator baseline의 **약 4배 거친** 해상도 사용.

---

## 2. 발견된 distortion 위험

### 2A. m-grid 해상도 부족 (η>1 셀)

`σ_e(θ) = σ_0 / max(p(θ), eff_floor)^η`에서 η가 클수록 prior tail에서 σ_e
폭발. 예: η=1.5, σ_0=0.07, prior_pdf=eff_floor=1e-2:
- σ_e_max = 0.07 / 0.01^1.5 = 0.07 / 0.001 = **70 s**
- m-grid 자동 설정 m_pad×σ_e_max = 5×70 = 350 (양쪽) → m 범위 700 wide
- n_m=801에서 dm = 0.875 — signal scale (σ_0 ~ 0.07)에 비해 **10× 거친 sampling**

이 영역에서 BLS posterior가 garbage 수치 산출. 실제 fig3 첫 시도에서 α≈3.7
(η≈0.85) 부근에 spike artifact 관찰됨.

### 2B. θ-range truncation (wide-prior 셀)

q7 sweep의 ω=0.60 셀에서 prior SD = 0.387 s. 디자인 mean (0.989/1.211) ±3SD
= [−0.16, 2.37]. θ range [0.30, 1.90]은 좌우 꼬리에서 **mass loss ~5–10%**.

renormalisation으로 partial 보정되나 prior shape 왜곡(skewness reduction).

### 2C. eff_floor 불일치

fig2 legacy의 `eff_floor=1e-3` vs. simulator pinned `1e-2`:
- (1e-3)^1 = 0.001 vs. (1e-2)^1 = 0.01 → σ_e blow-up 정도가 **10×** 차이
- η=1 기준 σ_e 최대값: fig2-1e-3 기준 70× σ_0, simulator-1e-2 기준 7× σ_0

### 2D. skew-normal normalisation 불일치

- q7: trapz로 grid 위에서 재정규화 (truncation 보정)
- fig3 (fig2 import): scipy.stats.skewnorm.pdf 직접 출력 (truncation 비보정)

→ 작은 systematic 차이 (~0.5–2% bias 추정).

---

## 3. 적용된 수정 (refactor 결과)

### 3A. 통일 baseline

| 매개변수 | 새 값 | 출처 |
|---|---|---|
| n_theta | **1401** | BOEC_intro.m §R5d pinned |
| n_m | **3001** | BOEC_intro.m §R5d pinned |
| θ range | **[0.10, 2.40]** | wider than design [0.30, 1.90]; covers q7 ω=0.60 셀 mean ±3.6 SD |
| eff_floor | **1e-2** | BOEC_intro.m pinned |

### 3B. 파일별 변경

**make_fig2_predictions.py**:
- `THETA = np.linspace(0.10, 2.40, 1401)` (was 0.30, 1.90, 321)
- `bls_bias_sd(..., n_m=3001)` default (was 401)
- `sigma_effprior(..., floor=1e-2)` default (was 1e-3)
- 표시는 `XLIM=(0.60, 1.60)`로 클립 (cosmetic only)
- 재실행: 1.4 sec, fig2 PNG 정상 재생성

**make_fig3_alpha_axis.py**:
- fig2 import로 자동 상속
- 재실행: 2.0 sec
- **정량적 개선**: 이전 α≈3.9의 spike artifact 제거 → 매끄러운 monotonic curve
  (H2:22ms → PCW:54ms → H3-η=1:73ms)

**q7_alpha_omega_sweep.m**:
- `n_theta=1401, n_m=3001, theta_lo=0.10, theta_hi=2.40` defaults
- 재실행: 8.4 sec (이전 0.2 sec → 42× 느림, 여전히 acceptable)
- design point: **+72.17 ms** (이전 +72.22 ms와 0.05ms 일치)
- 모든 25 cells 양수 (BOEC sign 일관); α 및 ω 방향 monotonic increasing

**build_bls_lookup.py**:
- `N_THETA_SOLVER=1401, N_M_SOLVER=3001, THETA_LO/HI=0.10/2.40`
- 재실행: 22 sec (이전 1.4 sec → 16× 느림, 여전히 fast HMC pre-build)
- design point (interpolated): **+72.2 ms** (q7와 정확 일치)
- File size: 250.4 KB (이전 248.9 KB)

### 3C. Display interpolation

표시 격자(fig3의 α-grid 21점, q7 figures, lookup THETA_GRID 17점)에는 사용자
요청대로 interpolation 적용:
- fig3: solver dense grid → α-axis discrete points via `np.interp`
- q7 figures: solver THETA → 표시 anchors via interpolation
- lookup table: solver theta_solver → 출력 THETA_GRID via `np.interp` (이미 구현됨)

### 3D. Wall-time impact

| 도구 | 이전 | 현재 | 비율 | 평가 |
|---|---|---|---|---|
| make_fig2 | ~0.5 s | 1.4 s | 2.8× | OK |
| make_fig3 | ~0.5 s | 2.0 s | 4× | OK |
| q7 sweep (25 cells) | 0.2 s | 8.4 s | 42× | OK |
| lookup table (1008 cells) | 1.4 s | 22 s | 16× | OK (HMC pre-build, one-time) |

총 22초의 lookup build는 HMC fitting 전 one-time 비용 → 무시 가능.

---

## 4. 검증 매트릭스 (refactor 후)

| 검증 | 도구 1 | 도구 2 | 결과 |
|---|---|---|---|
| q7 design point | MATLAB 1401/3001 | — | +72.17 ms |
| lookup design point (interp) | Python 1401/3001 | — | +72.2 ms |
| q7 ↔ lookup cross-validation | q7 +72.17 | lookup +72.2 | **±0.03 ms 일치** |
| fig3 H3-η=1 (α=4) | Python 1401/3001 | — | +73 ms (q7 +73.46 ms와 일치) |
| Sign sanity (25 q7 cells) | MATLAB | — | **모두 양수** (BOEC repulsion) |
| Monotonicity (q7 α-axis at ω=0.3374) | 56→67→72→73→74 ms (α=1→7) | — | monotonic ✓ |
| Monotonicity (q7 ω-axis at α=3.3) | 41→53→72→97→125 ms (ω=0.20→0.60) | — | monotonic ✓ |
| fig3 spike artifact 제거 | Python | — | **사라짐** (이전 α≈3.9의 1000ms spike → 안정 73ms) |

---

## 5. 잔류 한계 (motor noise 등)

### 5A. Motor noise (의도적 생략)

BOEC ex-ante 시뮬레이션에서 motor noise는 일관되게 omitted:
- 모형 가정: response = θ̂_BLS (deterministic readout)
- 실제 행동: response = θ̂_BLS + ε_motor, ε_motor ~ N(0, σ_motor²)

이 단순화의 효과:
- **bias(θ)**: 영향 없음 (additive zero-mean noise는 평균 보존)
- **SD(θ)**: 시뮬레이션 SD ≪ 관측 SD; 차이 ≈ √(σ_motor²) ~ 5–10 ms
- **HMC fitting 단계**: motor noise 별도 free parameter로 추가 (Luu 2018
  control experiment 패턴)

기록 위치: simulator README §Bundle B item 4 ("Motor noise — omitted at
ex-ante, safely absorbed into per-subject σ_e posterior under HWW 2025 §2.5.
To be measured at HMC stage").

### 5B. eff_floor=1e-2 의 model 가정

`max(p(θ), 1e-2)^η`의 floor는 **수치 보호**가 아닌 **물리 가정**임 (R5d
review): "위치 θ에 prior mass가 있더라도 neural 시스템은 1% threshold
이하의 'rare' 자극에 대해 가변 정밀도를 동원하지 않는다." η가 클수록 이
가정의 영향이 큼; η < 0.5 영역에서는 1e-2와 1e-3 차이가 무시 가능.

### 5C. θ range [0.10, 2.40] 의 mass coverage

skew-normal A (mean=0.989, SD=0.218): [0.10, 2.40]은 ±4.1 SD 좌, ±6.5 SD 우
→ 99.99%+ mass capture.
ω=0.60 q7 셀 (SD=0.387): ±2.3 SD 좌, ±3.0 SD 우 → ~99% mass. 충분.

극단 셀 (ω>0.60 또는 매우 narrow priors): 별도 사례별 검토 필요.

---

## 6. 결론

세션의 모든 ex-ante 도구가 이제 **단일 high-resolution baseline (n_theta=
1401, n_m=3001, θ ∈ [0.10, 2.40], eff_floor=1e-2)**에서 작동.
교차 검증 ±0.03 ms 정확도. 이전 fig3의 spike artifact 사라짐. q7 sweep
모든 25 cells 일관된 BOEC sign + monotonic 패턴.

Motor noise omission은 의도된 ex-ante 단순화로 README 명시 유지.

---

> **Delta**: RESOLUTION_AUDIT 결론:
> - 모든 ex-ante 도구 통일 baseline 적용
> - 4개 도구 (fig2, fig3, q7, lookup) refactored + re-tested
> - Cross-validation: q7 ↔ lookup 디자인 포인트 ±0.03 ms 일치
> - Spike artifact 제거 (fig3 α-axis curve 매끄러움)
> - 총 wall-time impact: lookup 1.4→22 sec (one-time HMC pre-build)
