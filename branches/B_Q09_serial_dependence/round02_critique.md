# B_Q09 R2 — Persona critique
## [B9R2] 2026-04-18

round01_findings.md에 대한 3인 전문가 페르소나 비평.

---

## Persona 1: Cicchini 입장 (sensory carryover 전문가)

**비평 핵심**: SC 방향 불일치 문제를 과소평가했다.

round01은 재현 과제에서 SC가 "attractive"라고 주장하지만, Wiener 2014와 Bertolasi 2025는 동일 시간 지각 맥락에서 **contrastive** SC를 보고한다. 이 불일치는 단순히 "과제 유형 차이"로 해소되지 않는다.

*구체적 문제*:
1. Wang 2023의 "attractive" 효과는 순수 지각적 SC인가, 아니면 재현 과제의 운동-지각 혼합인가? Wang 스스로 "motor memory 가능성"을 논의했다 (Wang 2023, §Discussion). SC를 순수 감각 채널로 분리하지 않고 "attractive = sensory carryover"로 등치시키는 것은 과도하다.
2. Cicchini 2018의 ideal observer 공식 ($w_{prev} = \sigma^2_{curr}/(\sigma^2_{curr} + d^2)$)은 orientation 자극을 기반으로 한다. **지속시간은 cardinal vs. oblique와 같은 신뢰도 변이가 없다** — 이 공식의 직접 전이를 정당화하는 근거가 round01에 없다.
3. SC 오염 추정(7.7%)이 낙관적으로 보인다. Wang 2023 half-amplitude를 우리 자극 범위(≈0.44–1.76s)에 적용하면 half-amplitude ≈ 18–22ms가 적절하다. 이를 b=0.077 slope으로 변환한 것이 맞는가? (half-amplitude와 regression slope는 서로 다른 메트릭)

**요구 수정**: SC attractive vs. contrastive의 과제 × 모달리티 × 방법 상호작용 표 필요. half-amplitude와 regression slope의 단위 변환 명확화 필요.

---

## Persona 2: Wiener 입장 (temporal carryover 전문가, decisive 입장)

**비평 핵심**: DC 효과를 과소추정했다. 232ms PSE shift는 신호(예상 BOEC bias)의 **3–4배**다.

*구체적 문제*:
1. 오염 추정에서 "β_DC ≈ 0.04"를 사용했지만 이 수치의 출처가 불명확하다. Cheng 2024는 PSE shift = 232ms (d=0.939)를 보고하는데, 이것이 인터리브 설계에서 어떻게 반응 단위의 slope으로 변환되는지 논리가 빠져 있다. 실제 continuous reproduction에서 DC slope은 β≈0.04 아닌 **β≈0.15–0.30** (Wiener 2014 Bayesian model에서 memory prior weight M≈13 시행)일 수 있다.
2. "50% 임계값" 판정에서 기준이 되는 분모(blocked design에서의 SD)를 계산하지 않았다. **Blocked 설계의 within-condition SD와 interleaved의 cross-condition DC를 비교**해야 한다 — 현재는 interleaved 오염만 계산했다.
3. 더 근본적으로: **DC는 단순 trial-to-trial 오염이 아니다**. Wiener 2014의 Bayesian memory prior는 M≈13 시행에 걸쳐 exponential decay로 오염이 축적된다. 700 시행 세션에서 인터리브 A-R 교대는 지속적 "A→R 오염"과 "R→A 오염"이 동시에 작용하여 **양쪽 bias를 모두 억압**할 수 있다.

**요구 수정**: 
- DC slope 추정의 명확한 출처 필요
- Blocked 설계의 within-block DC 크기 추산 (비교 기준점 확보)
- 다중 시행 누적 DC 모델 (exponential decay over M≈13 trials) 고려

---

## Persona 3: Wu 입장 (motor-response coupling 전문가, BRAC 이론)

**비평 핵심**: Motor coupling의 함의를 인터리브 설계에 유리한 쪽으로 잘못 해석했다.

*구체적 문제*:
1. round01은 "A/R 모두 재현이므로 motor coupling 관점에서 중립"이라고 결론 내렸다. 그러나 Wu 2026 BRAC 이론에 따르면 **event file에는 자극 지속시간 + 반응 지속시간이 함께 결합**된다. A 조건 (긴 기댓값) vs. R 조건 (짧은 기댓값)에서 **반응 지속시간 분포가 다르다** → A/R 조건 event file은 구별된다 → cross-condition 재활성화는 event file 불일치로 오히려 **SD 억제**로 이어질 수 있다.
2. Cheng 2024의 과제 유형 효과(d=0.652)는 "Time vs. Direction" 과제 전환에서 나왔다. A/R 조건 전환은 "Duration Reproduction vs. Duration Reproduction"이지만 **분포 파라미터**가 다르다. 이것이 "동일 과제"로 취급되어야 하는지 — 또는 분포 차이가 일종의 암묵적 "task switch"처럼 작용하는지 — 검증이 필요하다.
3. Cheng thesis Ch. 4 (fMRI): passive viewing (≈ no-go)이 sequential bias를 감소시킨다. 우리 설계에서 washout 시행을 no-go 방식으로 구성하면 SD를 0에 가깝게 억제할 수 있다. **Washout 시행 설계 가이드라인**이 누락되어 있다.

**요구 수정**:
- A/R 조건 event file의 유사성 vs. 차이 분석 필요 (반응 duration 분포 오버랩)
- Washout 시행 설계 권장사항 추가
- DC + SC 오염이 A→R과 R→A 방향에서 대칭인지 비대칭인지 명확화

---

## 종합 비평 메모

3개 페르소나 비평을 교차하면:

| 이슈 | 심각도 | 해결 방향 |
|---|---|---|
| SC attractive/contrastive 불일치 (Cicchini 페르소나) | 중간 | Task × modality 표; motor-SC 혼합 가능성 명시 |
| DC slope 수치 출처 불명확 (Wiener 페르소나) | 높음 | β_DC=0.04 근거 재확인; M=13 누적 모델 |
| DC 50% 임계값 비교 기준 미설정 (Wiener 페르소나) | 높음 | blocked 설계에서의 within-block DC 추산 |
| Event file 이질성: A vs. R 반응 분포 차이 (Wu 페르소나) | 중간 | Response duration 분포 오버랩 추산 |
| Washout 시행 설계 기준 미제시 (Wu 페르소나) | 낮음 | No-go washout 권장사항 추가 |

round03 (fan-in synthesis)에서 해결해야 할 핵심 미해결 사항:
1. **DC slope을 연속 재현 과제에서 정확히 추산** — Wiener 2014 모델에서 유도
2. **Blocked 설계의 within-condition DC 계산** → interleaved의 cross-condition DC와 직접 비교
3. **50% 임계값 재검토** — 절대 크기 기준으로 재산출

---

> **Delta**: 3개 페르소나 비평이 round01의 (a) DC slope 추산 방법론 허점, (b) SC 방향 불일치 해소 부족, (c) blocked 설계 비교 기준 미설정을 지적했다. Round03 synthesis가 이 세 가지 취약점을 해소해야 accept 기준 충족.
