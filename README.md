# AI–PAGE Research Summary

> Working README for the AI–PAGE climate damage analysis project.  
> This repository documents the research design, data requirements, scenario structure, PAGE input strategy, and unresolved methodological issues.

---

# 0. Quick Status

## English

This project is currently in the **first-stage PAGE execution preparation phase**.

The first-stage analysis focuses on a **direct-only AI data-centre CO₂ shock**. It does not estimate the full climate effect of AI. The main unresolved tasks are:

1. confirming the PAGE CO₂ shock input structure through read-only code inspection,
2. documenting the exact source and calculation path for S1 electricity demand and EF values,
3. finalizing post-2040 extrapolation assumptions,
4. distinguishing clearly between fixed-EF counterfactual shocks and what-if mitigation scenarios.

Current judgment:

```text
B. Conditionally ready for first-stage PAGE runs
```

The project can move toward first-stage PAGE runs after confirming the model input format and output post-processing rules.

## 한국어

현재 이 프로젝트는 **1차 PAGE 실행 준비 단계**입니다.

1차 분석은 **AI 데이터센터 전력수요 증가에 따른 직접 CO₂ shock**에 한정합니다. AI의 전체 기후효과를 추정하는 연구가 아닙니다. 현재 남은 주요 과제는 다음과 같습니다.

1. Codex read-only inspection을 통해 PAGE의 CO₂ shock 입력 구조를 확인하는 것,
2. S1 전력수요와 EF 값의 원자료 및 계산 경로를 문서화하는 것,
3. 2040년 이후 외삽 가정을 최종 정리하는 것,
4. fixed-EF counterfactual shock과 what-if mitigation scenario를 명확히 구분하는 것입니다.

현재 판정:

```text
B. 조건부로 1차 PAGE 실행 가능
```

PAGE 입력 형식과 결과 후처리 규칙을 확인한 뒤 1차 실행으로 넘어갈 수 있습니다.

---

# 1. Repository Purpose / 저장소 목적

## English

This repository organizes the current research design, data requirements, PAGE input structure, and remaining tasks for the AI–PAGE analysis.

The main goals are:

1. to document the current scenario design,
2. to track the data required for constructing AI-related CO₂ shocks,
3. to clarify what has been decided and what remains uncertain,
4. to prepare inputs for PAGE model runs,
5. to support handoff to Codex or other code-inspection tools.

This is a **research workflow and documentation repository**, not a final paper repository.

## 한국어

이 저장소는 AI–PAGE 분석을 위한 연구 설계, 필요한 데이터, PAGE 입력 구조, 남은 작업을 정리하기 위한 작업용 저장소입니다.

주요 목적은 다음과 같습니다.

1. 현재 시나리오 설계를 문서화,
2. AI-related CO₂ shock 산정에 필요한 데이터 추적,
3. 확정된 사항과 미확정 사항 구분,
4. PAGE 실행용 입력자료 준비,
5. Codex 또는 코드 점검 도구에 넘길 인계자료 작성.

이 저장소는 **최종 논문 저장소가 아니라 연구 워크플로우 및 문서화 저장소**입니다.

---

# 2. Current Research Scope / 현재 연구 범위

## English

The first-stage analysis focuses on the **direct CO₂ emission shock from AI-related data-centre electricity demand growth**.

Excluded from the first-stage analysis:

- AI indirect effects,
- rebound effects,
- GDP or productivity effects,
- policy costs,
- cost-effectiveness analysis,
- full energy-system optimization.

PAGE model settings such as ECS, discount rate, and GDP pathway are kept fixed. Only the CO₂ emission pathway is externally shocked.

## 한국어

1차 분석은 **AI 관련 데이터센터 전력수요 증가에서 발생하는 직접 CO₂ 배출 shock**에 초점을 둡니다.

1차 분석에서 제외하는 내용은 다음과 같습니다.

- AI 간접효과,
- 반등효과,
- GDP 또는 생산성 효과,
- 정책비용,
- 비용효과성 분석,
- 전체 에너지시스템 최적화.

PAGE의 ECS, 할인율, GDP 경로 등 기존 모형 설정은 유지하고, 외부에서 구성한 CO₂ emission pathway shock만 추가합니다.

---

# 3. Scenario Structure / 시나리오 구조

## English

| Scenario | Description | PAGE Input Change | Interpretation |
|---|---|---|---|
| S0 Reference | PAGE baseline without AI shock | AI-related CO₂ shock = 0 | No-AI-shock baseline |
| S1 AI Baseline | AI-era data-centre electricity growth converted into CO₂ shock | Additional electricity demand × regional EF | Fixed-EF counterfactual direct shock |
| S2 Clean Procurement | Same electricity demand, lower effective emission factor | EF reduction | What-if mitigation scenario |
| S3 Efficiency Standard | Same AI computing demand, lower facility electricity demand | Electricity demand reduction | What-if mitigation scenario |
| S4 Smart Siting | Partial redistribution of additional demand to lower-carbon or grid-available regions | Regional load reallocation / average EF reduction | What-if mitigation scenario |

Interpretation:

- S1 = electricity demand growth shock,
- S2 = effective emission factor reduction shock,
- S3 = efficiency-related electricity demand reduction shock,
- S4 = regional allocation / siting shock.

## 한국어

| 시나리오 | 설명 | PAGE 입력 변화 | 해석 |
|---|---|---|---|
| S0 Reference | AI shock이 없는 PAGE 기준선 | AI-related CO₂ shock = 0 | no-AI-shock 기준선 |
| S1 AI Baseline | AI-era 데이터센터 전력수요 증가를 CO₂ shock으로 변환 | 추가 전력수요 × 지역별 EF | fixed-EF counterfactual direct shock |
| S2 Clean Procurement | 동일 전력수요를 더 낮은 유효 배출계수의 전력으로 조달 | EF 감소 | what-if 완화 시나리오 |
| S3 Efficiency Standard | 동일 AI 컴퓨팅 수요를 더 낮은 시설 전력수요로 처리 | 전력수요 감소 | what-if 완화 시나리오 |
| S4 Smart Siting | 추가 수요 일부를 저탄소·계통여유 지역으로 재배치 | 지역별 부하 배분 변화 / 평균 EF 감소 | what-if 완화 시나리오 |

해석:

- S1 = 전력수요 증가 shock,
- S2 = 유효 배출계수 감소 shock,
- S3 = 효율개선에 따른 전력수요 감소 shock,
- S4 = 지역 배분 또는 입지 전환 shock.

---

# 4. What-if Scenario Parameters / What-if 시나리오 파라미터

## English

A **what-if scenario parameter** is not an empirically estimated policy-effect coefficient. It is a hypothetical parameter used to ask:

> If a certain technical or policy-relevant condition were achieved, how would the PAGE-based climate damage results change?

In this project, S2–S4 parameters are what-if parameters.

| Scenario | Parameter | Meaning | Safe Interpretation |
|---|---|---|---|
| S2 Clean Procurement | `α_clean` | Proportional reduction in effective EF | If clean procurement lowers effective EF by X%, PAGE damages change by Y |
| S3 Efficiency Standard | `β_efficiency` | Proportional reduction in additional electricity demand | If efficiency improvement reduces additional demand by X%, PAGE damages change by Y |
| S4 Smart Siting | `λ_siting` | Share of flexible demand shifted to lower-carbon or grid-available regions | If X% of additional load is shifted, PAGE damages change by Y |
| Persistence path | `m_t` | Fraction of 2030 shock that remains after 2040 | If the shock persists at level X, long-run PAGE damages change by Y |

These parameters should not be described as:

- policy effects,
- causal effects,
- estimated effectiveness,
- empirical treatment effects.

They should be described as:

- what-if scenario parameters,
- hypothetical mitigation parameters,
- scenario-based sensitivity parameters.

Recommended wording:

> S2–S4 are specified as what-if mitigation scenarios rather than estimated policy effects. The parameters represent hypothetical changes in effective emission intensity, electricity demand, or regional allocation, and the results should be interpreted as scenario-based sensitivity outcomes.

## 한국어

**what-if 시나리오 파라미터**는 관측자료로 추정한 정책효과 계수가 아닙니다. 이는 다음 질문에 답하기 위해 연구자가 설정하는 가정값입니다.

> 특정 기술적 조건 또는 정책 관련 조건이 달성된다면 PAGE 기반 기후피해 결과가 어떻게 달라질까?

현재 연구에서 S2–S4의 계수는 what-if 파라미터입니다.

| 시나리오 | 파라미터 | 의미 | 안전한 해석 |
|---|---|---|---|
| S2 Clean Procurement | `α_clean` | 유효 배출계수의 비례적 감소율 | clean procurement로 유효 EF가 X% 낮아진다면 PAGE 피해비용이 Y만큼 변함 |
| S3 Efficiency Standard | `β_efficiency` | 추가 전력수요의 비례적 감소율 | 효율개선으로 추가 수요가 X% 줄어든다면 PAGE 피해비용이 Y만큼 변함 |
| S4 Smart Siting | `λ_siting` | 유연한 부하 중 저탄소·계통여유 지역으로 이동하는 비율 | 추가 부하 X%가 이동한다면 PAGE 피해비용이 Y만큼 변함 |
| Persistence path | `m_t` | 2040 이후 2030 shock이 남아 있는 비율 | shock이 X 수준으로 지속된다면 장기 PAGE 피해비용이 Y만큼 변함 |

이 파라미터들은 다음처럼 표현하면 안 됩니다.

- 정책효과,
- 인과효과,
- 추정된 효과성,
- empirical treatment effect.

대신 다음처럼 표현하는 것이 안전합니다.

- what-if scenario parameters,
- hypothetical mitigation parameters,
- scenario-based sensitivity parameters.

권장 문장:

> S2–S4는 추정된 정책효과가 아니라 what-if 완화 시나리오로 설정한다. 각 파라미터는 유효 배출집약도, 전력수요, 지역 배분이 달라지는 가상 조건을 나타내며, 결과는 정책의 인과효과가 아니라 시나리오 기반 민감도 결과로 해석해야 한다.

---

# 5. Why This Is Not Policy-Effect Estimation / 왜 정책효과 추정이 아닌가

## English

The current design is **not policy-effect estimation** because it does not identify the causal impact of an actual policy using observed treatment and comparison groups.

Policy-effect estimation would typically require:

| Requirement | Meaning | Current Status |
|---|---|---|
| Actual policy or institutional change | e.g., a real PUE regulation or clean procurement mandate | Not used |
| Treatment group | Regions, firms, or facilities affected by the policy | Not defined |
| Comparison group | Similar units not affected by the policy | Not defined |
| Pre- and post-policy data | Observed outcome changes before and after implementation | Not used |
| Identification strategy | DID, IV, RDD, synthetic control, etc. | Not used |
| Control for confounders | Electricity prices, climate, power mix, demand growth, industrial structure | Not part of current design |

The PAGE model calculates climate damages conditional on input emissions pathways. It does not estimate how much a real policy changes the input emissions pathway.

Current design:

```text
Change input CO₂ shock pathway
→ PAGE calculation
→ Change in damage NPV and SCC
```

This structure supports **scenario-based damage assessment**, not causal policy evaluation.

Safe wording:

> This study does not estimate the causal effects of AI electricity policies. Instead, it evaluates how PAGE-based climate damage estimates change under alternative AI-related CO₂ shock scenarios.

## 한국어

현재 연구는 **정책효과 추정이 아닙니다.** 실제 정책의 인과효과를 처리집단과 비교집단을 통해 식별하는 구조가 아니기 때문입니다.

정책효과 추정이 되려면 일반적으로 다음 요소가 필요합니다.

| 필요 요소 | 의미 | 현재 연구의 상태 |
|---|---|---|
| 실제 정책 또는 제도 변화 | 예: 실제 PUE 규제, clean procurement 의무화 | 사용하지 않음 |
| 처리집단 | 정책 영향을 받은 지역·기업·시설 | 정의하지 않음 |
| 비교집단 | 정책 영향을 받지 않은 유사 단위 | 정의하지 않음 |
| 정책 전후 자료 | 정책 시행 전후의 관측 결과 변화 | 사용하지 않음 |
| 식별전략 | DID, IV, RDD, synthetic control 등 | 사용하지 않음 |
| 교란요인 통제 | 전력가격, 기후, 전력믹스, 수요증가, 산업구조 등 | 현재 설계에는 없음 |

PAGE는 주어진 배출경로에 조건부로 기후피해를 계산하는 모형입니다. PAGE 자체가 실제 정책이 배출경로를 얼마나 바꾸는지를 추정해주지는 않습니다.

현재 연구 구조는 다음과 같습니다.

```text
CO₂ shock 입력경로 변경
→ PAGE 계산
→ damage NPV 및 SCC 변화 확인
```

따라서 현재 연구는 **인과적 정책평가가 아니라 scenario-based damage assessment**입니다.

안전한 문장:

> 본 연구는 AI 전력정책의 인과효과를 추정하지 않는다. 대신 AI-related CO₂ shock 시나리오가 달라질 때 PAGE 기반 기후피해비용과 SCC가 어떻게 변화하는지를 분석한다.

---

# 6. What-if vs Counterfactual / What-if와 Counterfactual의 차이

## English

What-if scenarios and counterfactual scenarios overlap, but they are not identical.

| Concept | Meaning | Current Use |
|---|---|---|
| What-if scenario | A broad hypothetical scenario asking what happens under alternative assumptions | Best for S2–S4 |
| Counterfactual scenario | A comparison against a clearly defined alternative state or baseline | Appropriate for S0–S1 comparison and fixed-EF S1 shock |

In this project:

- S0–S1 can be described as a **model-based counterfactual comparison**.
- S1 can be described as a **fixed-EF counterfactual CO₂ shock** relative to no-AI shock baseline.
- S2–S4 should be described as **what-if mitigation scenarios**, not estimated policy counterfactuals.

Recommended wording:

> S1 is constructed as a fixed-EF counterfactual CO₂ shock relative to the no-AI baseline, while S2–S4 are treated as what-if mitigation scenarios rather than estimated policy counterfactuals.

## 한국어

what-if 시나리오와 counterfactual 시나리오는 겹치는 부분이 있지만 동일한 개념은 아닙니다.

| 개념 | 의미 | 현재 연구에서의 사용 |
|---|---|---|
| What-if scenario | 대안적 가정하에서 결과가 어떻게 달라지는지 보는 넓은 의미의 가상 시나리오 | S2–S4에 적합 |
| Counterfactual scenario | 명확한 기준선 또는 대안 상태와 비교하는 반사실적 시나리오 | S0–S1 비교 및 S1 fixed-EF shock에 적합 |

현재 연구에서는 다음처럼 구분하는 것이 안전합니다.

- S0–S1은 **모형 기반 counterfactual comparison**으로 표현 가능,
- S1은 no-AI 기준선 대비 **fixed-EF counterfactual CO₂ shock**으로 표현 가능,
- S2–S4는 추정된 정책 counterfactual이 아니라 **what-if mitigation scenarios**로 표현하는 것이 적절합니다.

권장 문장:

> S1은 no-AI 기준선 대비 fixed-EF counterfactual CO₂ shock으로 구성한다. 반면 S2–S4는 추정된 정책 counterfactual이 아니라 what-if 완화 시나리오로 해석한다.

---

# 7. S1 CO₂ Shock Calculation / S1 CO₂ Shock 계산 방식

## English

## 7.1 Core idea

The S1 CO₂ shock is **not directly copied from an IEA data-centre emissions projection**.

Instead, it is a researcher-calculated **fixed-EF counterfactual direct emission shock** constructed as:

```text
Additional data-centre electricity demand × regional power-sector average EF
```

The purpose is to create an **incremental shock** that can be added to the PAGE baseline emissions pathway.

## 한국어

## 7.1 핵심 개념

S1 CO₂ shock은 **IEA의 데이터센터 배출전망을 그대로 복사한 값이 아닙니다.**

대신 다음 방식으로 연구자가 계산한 **fixed-EF counterfactual direct emission shock**입니다.

```text
데이터센터 추가 전력수요 × 지역별 power-sector average EF
```

이 방식의 목적은 PAGE baseline 배출경로에 외생적으로 추가할 수 있는 **incremental shock**을 만드는 것입니다.

---

## English

## 7.2 Formula

```text
E_inc_TWh = E_DC_TWh_2030 - E_DC_TWh_2024

shock_MtCO2 = E_inc_TWh × EF_gCO2_kWh × 0.001
```

Unit conversion:

```text
1 TWh × 1 gCO₂/kWh = 0.001 MtCO₂
```

Reason:

- 1 TWh = 10^9 kWh,
- multiplying by gCO₂/kWh gives 10^9 gCO₂,
- 1 MtCO₂ = 10^12 gCO₂,
- therefore 10^9 / 10^12 = 0.001.

## 한국어

## 7.2 계산식

```text
E_inc_TWh = E_DC_TWh_2030 - E_DC_TWh_2024

shock_MtCO2 = E_inc_TWh × EF_gCO2_kWh × 0.001
```

단위 변환:

```text
1 TWh × 1 gCO₂/kWh = 0.001 MtCO₂
```

이유:

- 1 TWh = 10^9 kWh,
- 여기에 gCO₂/kWh를 곱하면 10^9 gCO₂,
- 1 MtCO₂ = 10^12 gCO₂,
- 따라서 10^9 / 10^12 = 0.001입니다.

---

## English

## 7.3 Electricity demand data

The electricity demand variable should refer to **total data-centre electricity consumption**, not only IT electricity consumption.

Reason:

- IT electricity consumption includes servers, storage, and network equipment.
- Total electricity consumption includes IT electricity plus cooling, power conversion losses, and other facility-level electricity use.
- CO₂ emissions depend on total electricity drawn from the grid.

Working S1 values:

| Region | E_DC 2024 TWh | E_DC 2030 TWh | E_inc TWh |
|---|---:|---:|---:|
| United States | 183 | 426 | 243 |
| Europe | 68 | 114 | 46 |
| China | 102 | 277 | 175 |
| Asia Pacific excl. China | 48 | 101 | 53 |
| ROW residual | 15 | 27 | 12 |
| World check | 416 | 945 | 529 |

Regional construction:

```text
APAC excl. China = IEA Asia Pacific - China
ROW residual = World - United States - Europe - China - APAC excl. China
```

## 한국어

## 7.3 전력수요 데이터

S1의 전력수요 변수는 IT 전력소비만이 아니라 **데이터센터 total electricity consumption**을 사용하는 것이 적절합니다.

이유:

- IT electricity consumption은 서버, 스토리지, 네트워크 장비 등의 전력입니다.
- Total electricity consumption은 IT 전력에 냉각, 전력변환 손실, 기타 시설 전력을 포함합니다.
- CO₂ 배출은 전력망에서 실제로 끌어오는 총전력 사용량에 의해 발생합니다.

현재 S1 작업값:

| Region | E_DC 2024 TWh | E_DC 2030 TWh | E_inc TWh |
|---|---:|---:|---:|
| United States | 183 | 426 | 243 |
| Europe | 68 | 114 | 46 |
| China | 102 | 277 | 175 |
| Asia Pacific excl. China | 48 | 101 | 53 |
| ROW residual | 15 | 27 | 12 |
| World check | 416 | 945 | 529 |

지역 구성 방식:

```text
APAC excl. China = IEA Asia Pacific - China
ROW residual = World - United States - Europe - China - APAC excl. China
```

---

## English

## 7.4 EF data and shock calculation

Current EF values are WEO-derived power-sector average EFs.

| Region | E_inc TWh | EF gCO₂/kWh | Calculation | shock MtCO₂/year |
|---|---:|---:|---|---:|
| United States | 243 | 326.5 | 243 × 326.5 × 0.001 | 79.3 |
| Europe | 46 | 230.7 | 46 × 230.7 × 0.001 | 10.6 |
| China | 175 | 657.6 | 175 × 657.6 × 0.001 | 115.1 |
| Asia Pacific excl. China | 53 | 597.0 | 53 × 597.0 × 0.001 | 31.6 |
| ROW residual | 12 | 443.1 | 12 × 443.1 × 0.001 | 5.3 |
| World check | 529 | — | Sum of regional shocks | 242.0 |

Current S1 global additional shock:

```text
S1 2030 shock = approximately 242.0 MtCO₂/year
```

## 한국어

## 7.4 EF 데이터와 shock 계산

현재 EF 값은 WEO-derived power-sector average EF입니다.

| Region | E_inc TWh | EF gCO₂/kWh | 계산 | shock MtCO₂/year |
|---|---:|---:|---|---:|
| United States | 243 | 326.5 | 243 × 326.5 × 0.001 | 79.3 |
| Europe | 46 | 230.7 | 46 × 230.7 × 0.001 | 10.6 |
| China | 175 | 657.6 | 175 × 657.6 × 0.001 | 115.1 |
| Asia Pacific excl. China | 53 | 597.0 | 53 × 597.0 × 0.001 | 31.6 |
| ROW residual | 12 | 443.1 | 12 × 443.1 × 0.001 | 5.3 |
| World check | 529 | — | 지역별 shock 합계 | 242.0 |

현재 S1 글로벌 추가 shock:

```text
S1 2030 shock = 약 242.0 MtCO₂/year
```

---

## English

## 7.5 Why this differs from IEA data-centre emissions projections

IEA data-centre emissions projections estimate total data-centre-related emissions under assumptions about future electricity supply, demand growth, and power-sector decarbonization.

The S1 shock in this project is different. It estimates only the **incremental emissions associated with additional electricity demand** using a fixed or simplified EF assumption.

| Item | IEA data-centre emissions projection | S1 fixed-EF shock |
|---|---|---|
| Meaning | Total projected emissions from data-centre electricity use | Incremental CO₂ shock from additional electricity demand |
| Source | IEA projection | Researcher calculation using IEA electricity demand and WEO-derived EF |
| Power mix treatment | Future supply mix and decarbonization may be embedded | Uses fixed or simplified regional average EF |
| PAGE interpretation | Not directly additive to baseline without caution | Designed as an additional exogenous shock |
| Risk if misused | Double-counting baseline emissions | More appropriate for incremental PAGE shock input |

Recommended wording:

> The S1 CO₂ shock is not directly taken from IEA data-centre emissions projections. It is a fixed-EF counterfactual direct emission shock calculated by applying WEO-derived regional power-sector average emission factors to the IEA-based increase in data-centre electricity demand. The shock is interpreted as an incremental emissions pathway added externally to the PAGE baseline, not as a forecast of total data-centre emissions.

## 한국어

## 7.5 IEA 데이터센터 배출전망과 다른 이유

IEA의 데이터센터 배출전망은 미래 전력공급, 수요증가, 전력부문 탈탄소화 등을 반영한 데이터센터 전력사용 관련 총배출 전망입니다.

반면 현재 연구의 S1 shock은 **추가 전력수요 증가분에 따른 incremental emissions**만을 fixed 또는 단순화된 EF 가정으로 산정한 값입니다.

| 구분 | IEA 데이터센터 배출전망 | S1 fixed-EF shock |
|---|---|---|
| 의미 | 데이터센터 전력사용에서 발생하는 총배출 전망 | 추가 전력수요에서 발생하는 incremental CO₂ shock |
| 출처 | IEA 전망 | IEA 전력수요와 WEO-derived EF를 이용한 연구자 계산 |
| 전력믹스 처리 | 미래 공급믹스 및 탈탄소화가 반영될 수 있음 | fixed 또는 단순화된 지역 평균 EF 적용 |
| PAGE 해석 | 그대로 baseline에 더하면 주의 필요 | 외생적 추가 shock으로 설계 |
| 잘못 사용할 때 위험 | baseline 배출과 중복계산 가능 | incremental PAGE shock 입력에 더 적합 |

권장 문장:

> S1 CO₂ shock은 IEA의 데이터센터 배출전망을 직접 사용한 값이 아니다. 본 연구는 IEA 기반 데이터센터 전력수요 증가분에 WEO-derived regional power-sector average EF를 적용하여 fixed-EF counterfactual direct emission shock을 산정한다. 이 shock은 PAGE baseline에 외생적으로 추가되는 incremental emissions pathway로 해석하며, 데이터센터 총배출량 전망으로 해석하지 않는다.

---

# 8. EF Treatment / 배출계수 처리 방식

## English

## 8.1 Ideal EF source

The ideal approach would be to use the IEA Emissions Factors database directly, with the following conditions:

```text
indicator: CO₂ emissions per kWh of electricity
gas: CO₂ only
scope: electricity-only, not electricity + heat
unit: gCO₂/kWh
region/year: aligned with the S1 regional classification
```

## 한국어

## 8.1 이상적인 EF 출처

가장 이상적인 방식은 IEA Emissions Factors 데이터베이스에서 다음 조건을 만족하는 값을 직접 사용하는 것입니다.

```text
indicator: CO₂ emissions per kWh of electricity
gas: CO₂ only
scope: electricity-only, not electricity + heat
unit: gCO₂/kWh
region/year: S1 지역 구분과 일치
```

---

## English

## 8.2 Why WEO-derived EF is used here

The current project uses WEO-derived power-sector average EF instead of direct IEA Emissions Factors for three reasons.

| Issue | Explanation |
|---|---|
| Access limitation | Direct access to the IEA Emissions Factors package may be limited or difficult depending on licensing and file format |
| Regional alignment | The exact regional classification used here may not be available as ready-made electricity-only EF values |
| Reproducibility | EF values derived from WEO regional electricity generation and power-sector CO₂ emissions are easier to document and reproduce |

Therefore, the current EF is calculated as:

```text
EF_r = Power-sector CO₂ emissions_r / Electricity generation_r × 1000
```

These values should be described as:

```text
WEO-derived power-sector average EF
```

They should not be described as:

```text
IEA direct electricity-only EF
```

## 한국어

## 8.2 왜 WEO-derived EF를 사용하는가

현재 프로젝트는 IEA Emissions Factors 직접값 대신 WEO-derived power-sector average EF를 사용합니다. 이유는 세 가지입니다.

| 문제 | 설명 |
|---|---|
| 접근성 문제 | IEA Emissions Factors 패키지는 라이선스나 파일 형식에 따라 직접 접근·추출이 어렵거나 제한될 수 있음 |
| 지역구분 문제 | 현재 연구의 지역 구분과 정확히 일치하는 region-level electricity-only EF가 바로 제공되지 않을 수 있음 |
| 재현성 문제 | WEO의 지역별 전력생산량과 전력부문 CO₂ 배출량을 이용해 계산한 EF는 계산 경로를 문서화하고 재현하기 쉬움 |

따라서 현재 EF는 다음과 같이 계산합니다.

```text
EF_r = Power-sector CO₂ emissions_r / Electricity generation_r × 1000
```

이 값들은 다음처럼 표현해야 합니다.

```text
WEO-derived power-sector average EF
```

다음처럼 표현하면 안 됩니다.

```text
IEA direct electricity-only EF
```

---

## English

## 8.3 Strengths and limitations of WEO-derived EF

| Aspect | Explanation |
|---|---|
| Strength | Transparent calculation from electricity generation and power-sector CO₂ emissions |
| Strength | Easier alignment with regional PAGE/S1 structure |
| Strength | Easier global consistency check |
| Limitation | Not identical to official IEA electricity-only EF |
| Limitation | Average EF, not marginal EF |
| Limitation | Does not reflect data-centre-specific procurement |
| Limitation | Residual regions such as APAC excl. China and ROW contain greater uncertainty |

Recommended wording:

> Regional emission factors are calculated as WEO-derived power-sector average emission factors using regional electricity generation and power-sector CO₂ emissions. They are used as average grid emission factors for constructing direct data-centre electricity-demand shocks, not as data-centre-specific or marginal emission factors.

## 한국어

## 8.3 WEO-derived EF의 장점과 한계

| 구분 | 설명 |
|---|---|
| 장점 | 전력생산량과 전력부문 CO₂ 배출량으로 계산되어 산식이 투명함 |
| 장점 | S1/PAGE 지역 구조와 맞추기 쉬움 |
| 장점 | 글로벌 합계 검산이 쉬움 |
| 한계 | 공식 IEA electricity-only EF와 완전히 동일한 지표는 아님 |
| 한계 | marginal EF가 아니라 average EF임 |
| 한계 | 데이터센터 전용 전력조달 구조를 반영하지 못함 |
| 한계 | APAC excl. China 및 ROW 같은 잔차 지역은 불확실성이 더 큼 |

권장 문장:

> 지역별 배출계수는 WEO의 지역별 전력생산량과 전력부문 CO₂ 배출량을 이용해 산정한 WEO-derived power-sector average EF이다. 이는 데이터센터 전력수요 shock 산정을 위한 평균 전력망 배출계수로 사용되며, 데이터센터 전용 배출계수나 marginal emission factor로 해석하지 않는다.

---

# 9. Regional Classification / 지역 구분

## English

The current first-stage S1 master table uses the following regional structure:

| Region | Treatment |
|---|---|
| United States | Direct IEA region |
| Europe | IEA-style Europe, including EU and non-EU Europe |
| China | Direct IEA region |
| Asia Pacific excl. China | IEA Asia Pacific excluding China; India is included in this residual region |
| ROW residual | World residual after excluding the above regions |

Important note:

> The APAC region in this repository means **Asia Pacific excluding China**, not APAC excluding China and India. India is not separated as an independent region in the current S1 setup.

Selected APAC countries such as Korea, Japan, Singapore, Malaysia, and Australia may be used as policy or technical examples for S2–S4, but they are not used to construct the S1 regional electricity demand total.

## 한국어

현재 1차 S1 master table은 다음 지역 구분을 사용합니다.

| Region | 처리 방식 |
|---|---|
| United States | IEA 직접 지역 |
| Europe | EU와 비EU 유럽을 모두 포함하는 IEA식 Europe |
| China | IEA 직접 지역 |
| Asia Pacific excl. China | IEA Asia Pacific에서 China를 제외한 지역. India는 이 residual region에 포함 |
| ROW residual | 위 지역들을 제외한 World residual |

중요한 점:

> 이 저장소에서 APAC은 **Asia Pacific excluding China**를 의미합니다. APAC excluding China and India가 아닙니다. 현재 S1 구조에서는 India를 독립 지역으로 분리하지 않습니다.

한국, 일본, 싱가포르, 말레이시아, 호주 등 일부 APAC 국가는 S2–S4의 정책·기술 사례로 활용할 수 있지만, S1 지역별 전력수요 총량을 구성하는 데 사용하지 않습니다.

---

# 10. PAGE Analysis Horizon / PAGE 분석 기간

## English

The main reported result will focus on:

```text
discounted climate damage NPV to 2100
```

Longer-horizon outputs such as 2150 or 2300 may be calculated by PAGE but should be treated as long-horizon sensitivity results rather than the central result.

Reason:

PAGE can run to very long horizons, but AI-specific CO₂ shock extrapolation beyond 2040 is highly uncertain.

## 한국어

본문의 핵심 결과는 다음에 초점을 둡니다.

```text
2100년까지의 discounted climate damage NPV
```

PAGE는 2150년 또는 2300년까지 결과를 산출할 수 있지만, 이러한 장기 결과는 중심 결과가 아니라 장기 민감도 분석으로 처리하는 것이 적절합니다.

이유:

PAGE는 매우 장기까지 실행 가능하지만, AI-specific CO₂ shock을 2040년 이후까지 방어 가능하게 외삽할 근거가 부족하기 때문입니다.

---

# 11. Current Extrapolation Assumption / 현재 외삽 가정

## English

Current central persistence path:

| PAGE year | Central multiplier |
|---:|---:|
| 2030 | 1.0 |
| 2040 | 1.0 |
| 2050 | 0.7 |
| 2075 | 0.3 |
| 2100 | 0.1 |

This is not a forecast.

Keeping the 2040 shock equal to the 2030 shock does not mean data-centre electricity demand is assumed to stop growing. It means that additional demand growth and power-sector decarbonization / efficiency improvements are assumed to partially offset each other in the central PAGE input path.

Low and high persistence paths still need to be finalized.

## 한국어

현재 central persistence path는 다음과 같습니다.

| PAGE year | Central multiplier |
|---:|---:|
| 2030 | 1.0 |
| 2040 | 1.0 |
| 2050 | 0.7 |
| 2075 | 0.3 |
| 2100 | 0.1 |

이는 예측값이 아닙니다.

2040년 shock을 2030년과 동일하게 둔다는 것은 데이터센터 전력수요가 증가하지 않는다고 가정한다는 뜻이 아닙니다. 이는 2030 이후 추가 수요 증가와 전력부문 탈탄소화·효율개선이 central PAGE input path에서 일부 상쇄된다고 보는 가정입니다.

Low 및 high persistence path는 아직 최종 확정이 필요합니다.

---

# 12. Data Still Needed / 추가로 필요한 데이터

## English

## Priority 1

| Needed Data | Purpose |
|---|---|
| IEA Table A.4 page / table reference | Defend E_DC_TWh values |
| Regional electricity generation TWh | EF calculation |
| Regional power-sector CO₂ emissions Mt | EF calculation |
| EF calculation table | Defend EF values |
| PAGE AI shock variable name, unit, dimension, and time grid | Avoid implementation errors |

## Priority 2

| Needed Data | Purpose |
|---|---|
| IEA 2035 data-centre electricity demand cases | Support 2040 and post-2040 extrapolation discussion |
| IEA data-centre emissions 2030 / 2035 | Compare against S1 fixed-EF shock |
| S2 clean procurement evidence | Defend effective EF reduction parameters |
| S3 efficiency / PUE evidence | Defend efficiency parameters |
| S4 siting / grid availability evidence | Defend smart siting parameters |

## Priority 3

| Needed Data | Purpose |
|---|---|
| Beath et al. full-AI emissions sensitivity | Optional later full-AI sensitivity |
| Long-horizon PAGE output sensitivity | Appendix robustness |
| Output post-processing validation | Confirm discounted NPV, units, NaN handling |

## 한국어

## 우선순위 1

| 필요한 데이터 | 목적 |
|---|---|
| IEA Table A.4 페이지 / 표 번호 | E_DC_TWh 값 방어 |
| 지역별 전력생산량 TWh | EF 계산 |
| 지역별 전력부문 CO₂ 배출량 Mt | EF 계산 |
| EF 계산표 | EF 값 방어 |
| PAGE AI shock 변수명, 단위, 차원, time grid | 실행 오류 방지 |

## 우선순위 2

| 필요한 데이터 | 목적 |
|---|---|
| IEA 2035 데이터센터 전력수요 시나리오 | 2040 및 2040 이후 외삽 논의 보강 |
| IEA 데이터센터 배출량 2030 / 2035 | S1 fixed-EF shock과 비교 |
| S2 clean procurement 근거 | 유효 EF 감소 파라미터 방어 |
| S3 efficiency / PUE 근거 | 효율 파라미터 방어 |
| S4 siting / grid availability 근거 | smart siting 파라미터 방어 |

## 우선순위 3

| 필요한 데이터 | 목적 |
|---|---|
| Beath et al. full-AI emissions sensitivity | 후속 full-AI sensitivity 가능성 |
| 장기 PAGE output sensitivity | 부록 강건성 분석 |
| output post-processing validation | 할인 여부, 단위, NaN 처리 확인 |

---

# 13. Codex Read-Only Inspection Task / Codex 읽기 전용 점검 과업

## English

Before modifying PAGE code or generating final PAGE input files, Codex should inspect the repository in read-only mode.

Key questions:

1. Where is the AI-related CO₂ shock parameter defined?
2. What is the parameter name?
3. What is the unit?
4. Is the shock time-only or region-by-time?
5. Is the shock added to baseline emissions or does it overwrite the baseline?
6. What time grid does the model expect?
7. What CSV format is required?
8. Which runner script should be used for multiple AI scenarios?
9. Which output files should be used for damage NPV to 2100 and SCC?

Codex must not modify any source code during this inspection.

## 한국어

PAGE 코드를 수정하거나 최종 PAGE 입력파일을 만들기 전에, Codex는 read-only mode로 저장소를 점검해야 합니다.

핵심 질문:

1. AI-related CO₂ shock 파라미터는 어디에서 정의되는가?
2. 파라미터 이름은 무엇인가?
3. 단위는 무엇인가?
4. shock은 time-only인가, region-by-time인가?
5. shock은 baseline emissions에 더해지는가, 아니면 baseline을 덮어쓰는가?
6. 모형이 기대하는 time grid는 무엇인가?
7. 필요한 CSV 형식은 무엇인가?
8. 여러 AI 시나리오를 실행할 때 어떤 runner script를 써야 하는가?
9. damage NPV to 2100과 SCC 산정을 위해 어떤 output 파일을 써야 하는가?

이 점검 단계에서 Codex는 source code를 수정하면 안 됩니다.

---

# 14. Output Processing Checks / 결과 후처리 체크리스트

## English

Before reporting PAGE results, confirm the following:

| Check | Reason |
|---|---|
| Is damage NPV already discounted? | Avoid double discounting |
| What is the currency unit? | Prevent unit errors |
| What is the base year? | Correct interpretation |
| Which time index corresponds to 2100? | Correct truncation |
| How are NaN trials handled? | Consistent Monte Carlo summary |
| Are results mean, median, p05, p95? | Proper uncertainty reporting |
| Is S0 used as the correct baseline? | Correct difference calculation |

## 한국어

PAGE 결과를 보고하기 전에 다음 사항을 확인해야 합니다.

| 확인 항목 | 이유 |
|---|---|
| damage NPV가 이미 할인된 값인가? | 중복 할인 방지 |
| 화폐 단위는 무엇인가? | 단위 오류 방지 |
| 기준연도는 무엇인가? | 올바른 해석 |
| 2100년에 해당하는 time index는 무엇인가? | 올바른 기간 절단 |
| NaN trial은 어떻게 처리하는가? | Monte Carlo 요약 일관성 |
| 결과는 mean, median, p05, p95 중 무엇인가? | 불확실성 보고 방식 결정 |
| S0가 올바른 baseline으로 사용되는가? | 차이 계산 오류 방지 |

---

# 15. Main Limitations / 주요 한계

## English

The following limitations must be clearly stated in any paper or report based on this work:

1. The analysis is direct-only and does not estimate the full climate effect of AI.
2. Indirect effects, rebound effects, and GDP effects are excluded.
3. S2–S4 parameters are what-if scenario assumptions, not estimated policy effects.
4. The EF values are WEO-derived power-sector average factors, not direct IEA electricity-only EF values.
5. Post-2040 shock paths are extrapolation scenarios, not forecasts.
6. 2150 or 2300 results, if reported, should be interpreted only as long-horizon sensitivity results.

## 한국어

이 연구를 바탕으로 논문이나 보고서를 작성할 때 다음 한계를 명확히 밝혀야 합니다.

1. 본 분석은 direct-only 분석이며 AI의 전체 기후효과를 추정하지 않습니다.
2. 간접효과, 반등효과, GDP 효과는 제외합니다.
3. S2–S4 파라미터는 추정된 정책효과가 아니라 what-if 시나리오 가정입니다.
4. EF 값은 WEO-derived power-sector average factor이며, IEA direct electricity-only EF가 아닙니다.
5. 2040년 이후 shock path는 예측이 아니라 외삽 시나리오입니다.
6. 2150년 또는 2300년 결과를 제시할 경우 장기 민감도 결과로만 해석해야 합니다.

---

# 16. Recommended Methods Wording / Methods 권장 문장

## English

> This study constructs an AI-related direct CO₂ emission shock from projected data-centre electricity demand growth and evaluates its implications for PAGE-based climate damage estimates. S1 is specified as a fixed-EF counterfactual CO₂ shock relative to a no-AI-shock baseline. The shock is calculated by applying WEO-derived regional power-sector average emission factors to the increase in IEA-based regional data-centre electricity demand. S2–S4 are specified as what-if mitigation scenarios rather than estimated policy effects, representing alternative assumptions about clean procurement, efficiency improvement, and smart siting. Therefore, the results should be interpreted as scenario-based damage assessment and sensitivity analysis, not as causal policy evaluation.

## 한국어

> 본 연구는 전망된 데이터센터 전력수요 증가를 바탕으로 AI-related direct CO₂ emission shock을 구성하고, 이 shock이 PAGE 기반 기후피해비용에 미치는 함의를 분석한다. S1은 no-AI-shock 기준선 대비 fixed-EF counterfactual CO₂ shock으로 설정한다. 이 shock은 IEA 기반 지역별 데이터센터 전력수요 증가분에 WEO-derived regional power-sector average EF를 적용하여 산정한다. S2–S4는 추정된 정책효과가 아니라 clean procurement, efficiency improvement, smart siting에 대한 대안적 가정을 반영한 what-if 완화 시나리오로 설정한다. 따라서 본 연구의 결과는 인과적 정책평가가 아니라 시나리오 기반 피해비용 평가 및 민감도 분석으로 해석해야 한다.

---

# 17. Version Notes / 버전 기록

| Version | Description |
|---|---|
| v1 | Initial research summary |
| v2 | Added status labels, source tracking, output checks, and improved HTML structure |
| v3 | Added detailed explanations of what-if parameters, fixed-EF S1 shock calculation, EF treatment, and policy-effect limitations |

