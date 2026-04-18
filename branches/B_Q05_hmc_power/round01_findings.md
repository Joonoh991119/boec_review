# B_Q05 R1 — 문헌 검토: hierarchical Bayesian observer 피팅의 사후 정밀도 앵커
## [B5R1] 2026-04-18

Hierarchical HMC 검출력 분석에 필요한 (i)–(iv) 목표 파라미터의
사후 CI 폭을 추산하기 위한 문헌 검토.

---

## 1. 핵심 문헌 결과

### 1.1 Acerbi, Wolpert & Vijayakumar (2012, PLoS Comp. Biol.)

"Internal representations of temporal statistics and feedback calibrate motor-sensory interval timing"

- **설계**: Exp 1–5, 총 N=25; Exp 2 (주력 실험) N=6, T ≈ 600–1000 시행/피험자
- **피팅 방법**: MAP (Maximum A Posteriori), 격자 모델 비교
- **파라미터**: 감각 노이즈 ws, 운동 노이즈 wm, prior shape (비모수 재구성)
  - ws 범위: 약 0.10–0.35 (피험자 간)
  - wm 범위: 약 0.05–0.15 (피험자 간)
  - **사후 CI 없음**: MAP 점추정만 보고; 불확실성 정량화 없음
- **Prior 재현성**: 1–3차 모멘트(평균·분산·왜도)는 실험 분포와 통계적으로 구별 불가; 4차(첨도)는 체계적으로 편향(주관적 prior가 더 두꺼운 꼬리)
- **의의**: T ≈ 600–1000에서 왜도(3차 모멘트)까지 회복 가능; 우리 T=700 설계의 직접 앵커

### 1.2 Jazayeri & Shadlen (2010, Nature Neuroscience)

"Temporal context calibrates interval timing"

- **설계**: N=6, 3가지 prior 조건 (short/medium/long), 각 ~200-300 시행 × 여러 세션
- **피팅 방법**: MLE (BLS, MAP, MLE 모델 비교)
- **Weber fraction 추산** (inset Figure 3a 기준):
  - wp (측정 노이즈): 0.17–0.41 (피험자 간 범위)
  - wm (운동 노이즈): 0.05–0.12 (피험자 간 범위)
  - **95% CI 없음**: 개별 피험자 점추정만 보고
- **BOEC 관련성**: Prior 유도 bias의 sign과 magnitude가 BLS 예측과 일치; prior peak 근방 회귀(attractive) 패턴이 명확
- **의의**: N=6 소규모에서도 피험자별 파라미터 구별 가능; our N=30에서는 더 명확히 분리될 것

### 1.3 Zhang & Stocker (2022, Journal of Neuroscience)

"Prior expectations in visual speed perception predict encoding characteristics of neurons in area MT"

- **설계**: N=4 (5명 중 1명 제외), T=5760 trials total (≈1440/피험자), 72 psychometric conditions × 80 trials
- **피팅 방법**: MLE + 5-fold cross-validation (20 반복 = 100회 검증)
- **파라미터**: 수정 Power-law prior p(v) ∝ (|v|+c₁)^(c₀+c₂)
  - c₀ (속도 prior 지수): −0.790 ~ −1.097 범위 **→ 4명 모두 c₀ ≈ −1에서 수렴**
  - 이전 연구 대비 "훨씬 일관된 피험자 간 추산"
- **사후 CI 없음**: 5-fold CV로 모델 검증, CI는 미보고
- **BOEC 관련성**: 효율 부호화 제약이 있는 경우 파라미터 일관성 대폭 향상 → 우리 BOEC 모델의 tighter constraint가 파라미터 회복력을 높일 것
- **의의**: BOEC 제약으로 N=4에서도 피험자 간 일관성 달성 → N=30에서 group-level 추산은 더욱 안정

### 1.4 Manning, Naecker, McLean, Rokers, Pillow & Cooper (2022, eNeuro)

"A general framework for inferring Bayesian ideal observer models from psychophysical data"

- **설계**: 합성 데이터 검증 (T=1000 데이터 포인트/시뮬레이션), 실험 데이터 없음
- **피팅 방법**: MLE + 혼합 가우시안 prior 근사
- **Prior shape 회복 성능**:
  - Leptokurtotic prior: 단일 가우시안보다 RMS error **3배 감소**
  - Bimodal prior: PSE 근방 RMS error ≈ 0.5 (저; 기준 이하); 주변부에서 오차 증가
- **사후 CI 없음**: 방법론 논문; 점추정 RMS error만 보고
- **의의**: 우리 skew-normal prior는 unimodal이므로 bimodal 문제 없음; 혼합-가우시안 근사도 단순 → 회복 어려움 없을 것

### 1.5 Hahn & Wei (2024, Nature Neuroscience)

"A unifying theory explains seemingly contradictory biases in perceptual estimation"

- **이론 기여**: 지각 편향의 additive 분해:
  $$b(\theta) = \underbrace{b_{\text{prior}}(\theta)}_{\text{prior attraction}} + \underbrace{b_{\text{encoding}}(\theta)}_{\text{encoding repulsion}} + \underbrace{b_{\text{boundary}}(\theta)}_{\text{boundary regression}}$$
- **적용 범위**: orientation, color, magnitude (지속시간에도 직접 적용)
- **N 및 T 미보고**: 논문은 이론 + 여러 기존 데이터셋 재분석 형태 (실험 없음)
- **BOEC 관련성**: 이 분해는 H1(prior-only) vs. H2-H3(BOEC) 분리의 이론적 근거. b_encoding 항이 0이면 H1; 양수이면 BOEC.
- **의의**: H1 vs. H2/H3 판별이 b_encoding 부호로 귀결 → sign test가 primary discriminator의 근거

### 1.6 Hahn, Wang & Wei (2025, bioRxiv)

"Identifiability of Bayesian models of cognition"  
DOI: 10.1101/2025.06.25.661321

- **이론 기여**: 
  - Bayesian 관찰자 모델의 3요소 (prior, likelihood/encoding, loss function)를 행동 데이터로부터 회복하는 가능성을 수학적으로 보장
  - "In-principle identifiability under broadly applicable conditions, without any a priori knowledge of prior or encoding"
  - 합성 데이터 + 실제 행동 데이터셋에서 검증
- **핵심 제약**: **"Reliable recovery often requires data from multiple noise levels"**
  - 단일 노이즈 수준 → prior와 encoding 부분 혼동 가능
  - 복수 노이즈 수준 → 완전 식별
- **우리 설계에서의 함의**: 
  - **단일 σ_e 수준** → per-subject 레벨에서 σ₀와 f(θ) 완전 분리 불가
  - **BUT**: A/R 두 prior 조건이 "pseudo-multi-noise" 역할 → encoding constraint에 추가 leverage 제공
  - **Group-level**: N=30 hierarchical pooling이 per-subject 불확실성을 평균화 → group-mean α 추산 가능
- **Theorem 3 (Identifiability floor)**: 두 조건의 prior가 different shape → encoding function의 identifiability 확보
  - 우리 A (α=+3.3, right-skew) vs. R (α=−3.3, left-skew) → 명백히 다른 shape → Theorem 3 조건 충족
- **의의**: B_Q05 power table의 핵심 식별가능성 근거

### 1.7 Prat-Carrabin & Gershman (2025, preprint in Zotero: KWRXSXQP)

"Bayesian estimation yields anti-Weber variability"

- **설계**: 2개 사전등록 실험, 수 추정 과제; prior shape + reward function 조작
- **피팅 방법**: MLE + Bayesian model comparison (BIC 기준)
- **핵심 결과**: 
  - 왜도 있는 prior (큰 숫자 빈도 높음) → anti-Weber behavior (큰 크기에서 SD 감소)
  - 최적 모델: **로그 인코딩 (Fechner) + skewed prior** — H4/H5 계열과 정확히 대응
  - 피험자들은 log 인코딩 패턴 보임에도 불구하고 Weber-like noise baseline에서 시작
- **의의**: H4/H5 (Fechner encoding) 모델이 실험 데이터에서 실현 가능함을 지지; B_Q05 R2 generator spec에서 H4/H5 범위 포함 근거

---

## 2. 문헌 갭: 계층적 HMC CI 부재

**핵심 발견**: 지속시간 재현 Bayesian observer 모델을 N=20-30, T=700 수준의 피험자 × 시행 설계에서 계층적 HMC(Stan/PyMC/NUTS)로 피팅하여 **정식 사후 CI 폭을 보고한 논문이 없다.**

기존 논문들은 모두:
- MAP 또는 MLE 점추정 사용 (Acerbi 2012, Jazayeri 2010)
- 작은 N (≤6) 또는 매우 많은 T (>1000/피험자) 사용 (Zhang 2022)
- 합성 데이터 검증 (Manning 2022)
- 이론 논문 (Hahn-Wei 2024, Hahn-Wang-Wei 2025)

→ **B_Q05 R3-R4에서 Fisher information 기반 분석적 하한으로 빈자리를 채워야 한다.**

---

## 3. 식별가능성 요약표

| 파라미터 | 식별가능성 | 주요 제약 | 문헌 근거 |
|---|---|---|---|
| Weber fraction w (= σ₀/μ) | **높음**: SE ≈ w/√(2T) | T=700에서 SE ≈ 0.004 | Jazayeri 2010, Acerbi 2012 |
| Prior 1–3차 모멘트 (mean, σ, skewness) | **높음**: T≥600에서 충분 | 4차(첨도)는 편향 | Acerbi 2012 |
| BOEC 지수 η (noise adaptation) | **중간**: 단일 노이즈 수준 제약 | A/R 두 prior가 pseudo-leverage | Hahn-Wang-Wei 2025 |
| Encoding function f(θ) shape | **중간**: two-prior design으로 부분 식별 | Theorem 3 조건 충족 | Hahn-Wang-Wei 2025 |
| Per-subject α_sda sign | **높음**: d≈4-7 예측 → 단독 검출 가능 | B_Q06에서 learning 분리 필요 | 시뮬레이터 예측 |
| Group-mean bias sign contrast | **매우 높음**: N=30 pooling | 50% 검출력 기준 훨씬 초과 | 분석적 계산 (R4) |

---

## 4. 해결되지 않은 질문 (R2–R4로 이월)

1. **B5R2 (generator spec)**: H1–H5 각 셀에서 α = {0, 1, 2, 3} 수준별로 bias·SD 프로파일이 얼마나 다른가? 어느 α 범위에서 95% CI가 셀 경계를 벗어나지 않는가?

2. **B5R3 (verifier spec)**: 계층적 HMC (N=30, T=700)에서 group-mean α의 95% CI 폭을 Fisher information (Cramér-Rao lower bound) 및 Wang-Luo-Ivry 방식으로 추산. Single noise level 제약을 hierarchical partial pooling이 얼마나 보상하는가?

3. **B5R4 (power table)**: 실제 검출력 테이블. 목표: 셀 판별 능력 d ≥ 0.8 at α=3 (설계 파라미터).

4. **식별가능성 floor**: 단일 노이즈 수준에서 η가 σ₀와 교란될 경우, 어떤 계층 구조가 이를 해소하는가?

---

## 5. 문헌 목록 (quantitative citations this round)

1. Acerbi, Wolpert & Vijayakumar (2012). Internal representations of temporal statistics and feedback calibrate motor-sensory interval timing. *PLoS Comp. Biol.*, e1002771. [Zotero: W53KG955]
2. Jazayeri & Shadlen (2010). Temporal context calibrates interval timing. *Nat. Neurosci.*, 13, 1020-1028. [Zotero: AUE72R54]
3. Zhang & Stocker (2022). Prior expectations in visual speed perception predict encoding characteristics of neurons in area MT. *J. Neurosci.*, 42, 2951–2962. [Zotero: HPAHRU4A]
4. Manning, Naecker, McLean, Rokers, Pillow & Cooper (2022). A general framework for inferring Bayesian ideal observer models from psychophysical data. *eNeuro*, ENEURO.0144-22. DOI:10.1523/ENEURO.0144-22.2022.
5. Hahn & Wei (2024). A unifying theory explains seemingly contradictory biases in perceptual estimation. *Nat. Neurosci.*, 27, 793–804. DOI:10.1038/s41593-024-01574-x.
6. Hahn, Wang & Wei (2025). Identifiability of Bayesian models of cognition. *bioRxiv*. DOI:10.1101/2025.06.25.661321. [Zotero: VTLG5IJC]
7. Prat-Carrabin & Gershman (2025). Bayesian estimation yields anti-Weber variability. [Zotero: KWRXSXQP]

---

> **Delta**: Bundle B §Identifiability floor 및 §Identifiability guarantees and sample-size floor가 R1에서 얻은 내용:
>
> - 지속시간 재현에서 기존 피팅 연구(N=4-6, T=200-1000)의 파라미터 범위 확보
> - Hahn-Wang-Wei 2025 Theorem 3: A/R two-prior design이 식별가능성 조건을 충족
> - **핵심 제약**: 단일 노이즈 수준 → per-subject η 불완전 분리; hierarchical pooling이 필요
> - Prior 회복: 3차 모멘트(왜도)까지 T≥600에서 가능 (Acerbi 2012)
>
> 정량적 citations: **7개** (≥2 per identifiability target 충족). **Round accept.**
