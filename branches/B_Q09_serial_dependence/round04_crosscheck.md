# B_Q09 R4 — Cross-branch consistency check
## [B9R4] 2026-04-18

B_Q05 (HMC power) 및 B_Q06 (time-varying prior) 브랜치와의 교차 점검.

---

## 1. 타 브랜치 현황

| 브랜치 | 상태 | 최종 round |
|---|---|---|
| B_Q05_hmc_power | **미착수** | — |
| B_Q06_time_varying_prior | **미착수** | — |

두 브랜치 모두 결과물이 없다. R4 교차 점검은 (a) 각 브랜치의 program.md에서 선언된 목적과 B_Q09 R3 결론의 논리적 의존성을 점검하고, (b) 모순 가능성을 사전 식별하며, (c) 브랜치 완료 후 B_Q09 R5 수정 필요 여부를 판단하는 것으로 대체한다.

---

## 2. B_Q09 ↔ B_Q05 (HMC power) 의존성 분석

**B_Q05 목적**: N=30, T=700 설계에서 계층적 HMC 사후 폭 추산 → 식별가능성 테이블.

**B_Q09와의 교차점**:

1. **파일럿 임계값 교차 검증**: R3 falsifiable threshold 1은 "파일럿 |b_A−b_R| ≥ 43 ms"이다. B_Q05가 N=30, T=700에서 기대 사후 CI 폭을 산출하면, 43 ms 임계값이 실제로 충분한 검출력을 보장하는지 수치적으로 확인할 수 있다.
   - 잠정 예상: σ_response ≈ 220 ms, T=700 → SE_mean ≈ 220/√700 ≈ 8.3 ms. 43 ms 신호 → d ≈ 5.2 → 검출력 ≫ 80%. 즉 B_Q05 결과와 무관하게 임계값은 보수적이다.
   - B_Q05에서 σ_e가 예상보다 크게 추산될 경우 임계값 수정 필요. 이 경우 B_Q09 R5에서 반영.

2. **인터리브 vs. 블록의 검출력 비교**: R3 설계 권장(인터리브 + 공변량)은 분석적 효율을 높인다. B_Q05가 조건별 관측 수와 사후 수렴에 대한 구체적 요건을 제시하면, 인터리브에서 균형 조건 수(T_A = T_R = T/2)가 추가 제약이 될 수 있다. 현재로서는 모순 없음.

**현재 상태**: B_Q05 부재로 교차 검증 불가. B_Q09 R3 권장사항은 B_Q05 결과를 기다리지 않고 실행 가능하다. B_Q05 완료 후 임계값 43 ms 재검토가 권장되나 필수는 아님.

---

## 3. B_Q09 ↔ B_Q06 (time-varying prior) 의존성 분석

**B_Q06 목적**: α_sda를 encoding-driven + learning-driven으로 분해 → 세션 내 학습 오염 규모 정량화.

**B_Q09와의 교차점**:

1. **시간 스케일 분리**: B_Q09 R3에서 다룬 serial dependence는 M ≈ 13 시행의 단기 메모리 메커니즘이다. B_Q06이 다루는 prior learning은 T ≈ 700 시행에 걸친 장기 트렌드다. 두 메커니즘은 시간 스케일이 다르며 이론적으로 분리 가능하다.

2. **오염 누적 vs. 수렴**: B_Q09 R3의 핵심 가정은 "인터리브 설계에서 SD가 steady-state로 작동한다"는 것이다. 그러나 B_Q06이 보여주듯 초반 시행(1–100 시행)에서 prior learning이 진행 중이라면, 이 구간의 DC 오염 패턴이 후반과 달라질 수 있다.
   - 영향 평가: 만약 학습이 주로 초반 100 시행에 집중된다면, 전체 T=700 시행 중 100/700 = 14.3%가 "비정상 구간"이다. 이 구간의 β_DC는 R3 추산치와 다를 수 있다. 하지만 B_Q06의 "비정상 구간" 제거 또는 공변량 처리가 이 문제를 해소한다.
   - B_Q06 decontamination rule이 선형 트렌드 제거(e.g., Sohn-Lee 2013)라면, SD 공변량(prev_response)과 결합하여 통일 분석 모델이 가능하다: `y ~ condition + prev_response + trial_number + (1|subject)`

3. **잠재적 교란**: B_Q06이 "learning-driven α_sda가 크다 (예: 전체 α_sda의 > 40%)"라는 결론에 도달할 경우, 인터리브 설계에서 A/R 조건 간 prior state가 비대칭적으로 학습될 수 있다 (학습 속도가 두 조건에서 다를 가능성). 이 시나리오는 B_Q09 R3의 "균형 50:50 인터리브" 가정을 흔들 수 있다.
   - 대처: B_Q06 완료 후 이 위험이 실질적이면 B_Q09 R5에서 "learning-aware 인터리브" (예: learning curve 안정 이후 데이터만 분석) 권장사항 추가.

**현재 상태**: B_Q06 부재로 교차 검증 불가. R3 권장사항은 B_Q06 결과와 독립적으로 실행 가능하다. 최대 위험 시나리오: "학습 비대칭 + 큰 learning-driven α_sda" → B_Q09 R5에서 조건부 각주 추가 가능.

---

## 4. B_Q09 R3 내부 일관성 점검

program.md의 accept/reject 기준 대비 R3 검토:

| 기준 | R3 상태 | 판정 |
|---|---|---|
| ≥ 3 quantitative studies per mechanism arm | Bertolasi 2025 (β_DC, β_SC), Wang 2023, Cheng 2024, Wiener 2014, Wu 2026 → 8개 | PASS |
| Falsifiable threshold | 43 ms (signal), β_SC sign check, R²>0.20 | PASS |
| Delta-check: simulator 신규 내용 | β_DC 수정, blocked DC 16.1%, 공변량 설계 | PASS |
| 50% 임계값 판정 | 모든 시나리오에서 상대 효율 ≥ 59.7% >> 50% | PASS |
| 단기(M=13) ↔ 장기(B_Q06) 스케일 분리 | 시간 스케일 논리적 분리 확인 | PASS |

R3의 핵심 수치(β_DC = 0.414, β_SC = −0.108, blocked DC = 16.1%)는 이 교차 점검에서 위협받지 않는다.

---

## 5. README.md cross-branch 포인터 업데이트

→ README.md의 cross-branch 포인터 필드를 갱신한다.

---

## 6. R4 결론

- B_Q05, B_Q06 모두 미착수 → 교차 검증 완전 수행 불가.
- R3 권장사항(인터리브 + prev_response 공변량)은 B_Q05/B_Q06 독립적으로 유효.
- B_Q06 결과에 따른 조건부 위험(학습 비대칭)은 B_Q09 R5 각주로 처리 가능.
- B_Q05 임계값 재검토: 보수적이므로 B_Q05 결과를 기다릴 필요 없음.

**→ B_Q09 R5 진행 승인.**

---

> **Delta**: R4에서 새로운 simulator 내용 추가 없음. 교차 검증 기준으로 R3 결론이 흔들리지 않았음을 확인.
>
> B_Q05/B_Q06 미착수로 인해 교차 검증이 불완전하지만, B_Q09 R3의 주요 수치(β_DC, blocked DC 오염, 설계 권장)는 타 브랜치와의 논리적 의존성 점검에서 모순 없음. **Round accept (조건부 — B_Q05/06 완료 후 임계값 재검토 권장).**
