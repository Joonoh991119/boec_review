# B_Q09 R5 — Finalisation + simulator amendment proposal
## [B9R5] 2026-04-18

---

## 1. 브랜치 결론 요약 (R1–R4 통합)

**핵심 수치 (확정)**:

| 파라미터 | 값 | 출처 |
|---|---|---|
| β_DC (연속 재현) | 0.414 [0.35, 0.48] | Bertolasi et al. 2025 |
| β_DC (이분 변환 상한) | ~0.66 | Cheng et al. 2024, PSE shift 232ms |
| β_SC (재현, 순수 감각) | −0.108 [−0.18, −0.04] | Bertolasi et al. 2025 |
| Wiener memory span M | ≈ 13 시행 | Wiener et al. 2014 |
| BRAC cross-dist. 감쇠 | ≈ 25% | Wu et al. 2026 추산 |
| No-Go SC 소멸율 | 95% | Wang et al. 2023 |

**설계별 attenuation (보수 추정, contrastive SC)**:

| 설계 | |b_A−b_R| attenuation | 신호 보존율 |
|---|---|---|
| 인터리브, 공변량 없음 | 30.6% | 69.4% |
| **인터리브 + prev_response 공변량** | **≈ −11%** | **≥ 100%** |
| 블록 B=30, 공변량 없음 | 16.1% | 83.9% |

**설계 권장 (확정)**: 완전 인터리브 + prev_response_duration 공변량 통제.

**50% 임계값 판정**: 모든 시나리오에서 통과. 브랜치 accept.

---

## 2. Simulator amendment 제안

Bundle B item (viii) 현재 텍스트(줄 513–526)를 아래로 교체한다.

### 현재 텍스트
```
8. **IID trials** — no serial dependence, no trial-order effects,
   no motor-response carryover. Empirically violated in duration
   reproduction: sensory carryover (Cicchini, Mikellidou & Burr
   2018), decisional carryover (Li, Wang & Zaidel 2026),
   motor-response coupling (Wu et al. 2024), task-switching
   amplification (Cheng, Chen, Yang & Shi 2024), post-perceptual
   emergence (Bliss, Sun & D'Esposito 2017; Pascucci et al. 2023);
   Manassi, Murai & Whitney (2023) meta-analysis confirms the
   robustness of serial dependence across tasks. If trials are
   randomly interleaved between A and R conditions, the (b_A, b_R)
   sign pattern is attenuated by sequential carryover; if blocked,
   within-block carryover persists but does not cross-contaminate.
   The discriminator bands implicitly assume condition-blocked
   analysis.
```

### 교체 텍스트 (B9R5 amendment)
```
8. **IID trials** — no serial dependence, no trial-order effects,
   no motor-response carryover. Empirically violated in duration
   reproduction via three mechanisms: (a) *sensory carryover* (SC),
   which is **contrastive** in reproduction tasks [β_SC = −0.108,
   Bertolasi, Esposito, Vitale & Gori 2025]; Wang et al. (2023)
   report attractive-looking SC (b=0.077) that is 95% suppressed by
   No-Go, indicating motor-coupling contamination in that estimate;
   (b) *decisional carryover* (DC), assimilative [β_DC = 0.41–0.66:
   Bertolasi et al. 2025 regression, 0.414; Cheng, Chen, Yang & Shi
   2024 PSE shift 232ms, d=0.939, converting to ~0.66]; accumulated
   over M ≈ 13 trials (Wiener et al. 2014 Bayesian memory prior);
   (c) *motor-response coupling* via BRAC event-file reactivation
   [Wu, Serçe & Shi 2026], reduced ~25% for A/R cross-condition
   transitions due to response-duration distribution mismatch.
   Quantitative attenuation (B_Q09 review, 2026-04-18): interleaved
   50:50 A/R sustains **30–41% attenuation** of |b_A − b_R| without
   covariate; condition-blocked (B = 30 trials) sustains **16.1%**
   attenuation via Wiener-decay at transitions. Relative efficiency
   of interleaved vs. blocked = 70–83% (>50% criterion: passed).
   **Recommended design**: fully interleaved with
   `prev_response_duration` as a regression covariate; with
   covariate, DC is removed and net effect of contrastive SC
   enhances |b_A − b_R| by ~11%. Falsifiable pilot thresholds: (1)
   |b_A − b_R| ≥ 43ms; (2) β_prev_stimulus < 0 (contrastive SC); (3)
   covariate R² > 0.20. Fallback: blocked B = 30 + 7-trial washout
   per transition if pilot signal < 30ms or SC is attractive. The
   discriminator bands assume interleaved + prev_response-covariate
   analysis.
```

---

## 3. Amendment 적용 가이드

파일 위치: `boec_simulator/README.md`, 줄 513–526.

변경 범위: Bundle B item 8 전체 교체 (현재 14줄 → 교체 20줄).
인접 항목(7, 8 이후 단락)은 건드리지 않는다.

커밋 메시지 컨벤션:
```
[boec_simulator ← boec_review B9R5] Bundle B (viii) iid-trials: quantitative SD design recommendation

β_DC = 0.41–0.66 (Bertolasi 2025, Cheng 2024), β_SC = −0.108 contrastive
(Bertolasi 2025), blocked DC = 16.1% (Wiener M=13), interleaved efficiency
70–83% vs. blocked. Recommended: interleaved + prev_response covariate.
Three falsifiable pilot thresholds added.
```

---

## 4. B_Q09 브랜치 조기 수렴 확인

program.md §Budget:
- Round 3 accept 조건 충족 확인 (R3에서 수렴)
- Round 4: cross-branch 점검 (B_Q05/B_Q06 미착수 → 내부 일관성 확인으로 대체)
- Round 5: 시뮬레이터 수정 제안 (현재 문서)
- 5-round cap 내 완료

program.md §Failure handling 중 해당 없음:
- 3개 mechanism 모두 quantitative effect-size 확보 ✓
- 50% 임계값 비교: 70–83% ≥ 50% ✓ (interleaved acceptable)
- 문헌 자기모순(SC 방향): R3에서 해소됨 ✓

**B_Q09 브랜치 CLOSED. → B_Q05 R1 착수.**

---

> **Delta**: Bundle B item (viii) 교체 텍스트 확정. 수정 전 정성적 경고에서 수정 후 정량적 설계 권장으로 전환:
> β_DC range [0.41, 0.66], β_SC = −0.108 contrastive, blocked DC = 16.1%,
> interleaved 효율 70–83%, 공변량 권장, 3개 falsifiable threshold.
> 정량적 citations: 총 8개 (R1 목록 유지).
> **Round accept. 브랜치 종료.**
