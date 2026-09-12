# 지표와 데이터 기준

지식 기준일: 2026-09-12. 테이블 스키마는 변경될 수 있으므로 운영 쿼리 작성 전 현재 컬럼을 확인한다.

## 목차

- 지표 체계와 시간·코호트 기준
- 핵심 수치 원천과 `superset` 시트
- 핵심 테이블, 서비스·상태 판별, 견적 집계
- 수요 쏠림과 수요 구간 분석
- 계약·매출 기준과 SQL 작성 점검표

## 지표 체계

사업의 One Metric은 Lead → Contract다. 실무 목표는 35%이며 과거 BEP 참고값은 약 37%다. 계약률을 하나의 Sales 문제로만 보지 말고 아래 연결 지표로 분해한다.

| 지표 | 정의 | 주요 제외·주의사항 |
|---|---|---|
| Lead → Visit Complete | 유니크 방문완료 / 대상 유니크 Lead | 목표 80%. 대상과 취소 처리 기준 명시 |
| Visit Complete → Contract | 결제 계약 / 유니크 방문완료 | 품질 참고 목표 50%. 지정된 결제 이벤트 사용 |
| Lead → Contract | 결제 계약 / 유니크 Lead | Cohort와 Simple 동기간 집계 구분 |
| AQPR | 유효 제출 파트너 견적 / 명시된 대상 또는 방문완료 Request | 참여 Slot 최대 6개와 고객 노출 최대 4개를 구분. 매니저·플래너 제외 |
| 저견적 비율 | 유효 견적 2개 이하 Request / 견적 대상 Request | 전략 목표 0%. 견적 Row 수와 혼동하지 않음 |
| 6시간 내 견적 제출률 | 방문완료 뒤 6시간 안에 유효 견적이 제출된 Request / 견적 대상 Request | 운영 목표 50%. 시작·종료 Timestamp와 KST 명시 |
| 미추천 Request 비율 | 추천된 유효 견적이 0개인 Request / 고객 노출 대상 Request | 목표 0%. 추천 Flag와 노출 상태의 Source 확인 |
| 확정 견적 입력률 | 2시간 안에 최종 견적을 입력한 자동 참여 / 자동 참여 | 1초견적 Pilot 지표. Slot 참여를 완료로 세지 않음 |
| 방문완료 Volume | 방문완료 + 방문 전 취소 + No-show 예정 건 | 비율만이 아니라 구성 요소도 표시 |

## 핵심 수치 원천과 `superset` 시트

미소방문 핵심 수치의 기본 원천은 Google Sheet `daily number & Moving by Miso Metrics`다. 사용자가 별도 원천을 지정하지 않으면 다음 순서로 확인한다.

1. `superset`: 원천 Import와 일자·서비스별 집계, 계약·매출·Credit·GP의 핵심 데이터
2. `Moving by Miso Metrics(day)`, `Moving by Miso Metrics(week)`, `Moving by Miso Metrics(month)`: 기간별 표시 View
3. `Know your numbers(MVC)`, `cohort`, `MVC_cohort_rate`, `Month(Daily Contract Rate)`, `Month(Contract Conversion Rate)`: 목적별 계산 View
4. `Excellent Operation`, `daily processing 관리,`: 운영 품질과 Processing 점검
5. `Deals(hubspot)`, `Cross sell(hubspot)`: CRM·Cross-sell 보조 원천

`superset`의 확인된 필드군에는 `date`, `service_type`, `request_cnt`, `aqpr`, `quote_cnt`, `paid_quote_cnt`, `auto_quote_cnt`, `active_partner_cnt`, `active_customer_cnt`, `revenue`, `gross_profit`, `commission_due`, `day_contract_cnt`, `due_contract_cnt` 및 Credit·Refund 항목이 포함된다. Header 이름만 보고 사업 의미를 단정하지 않고 Source Query와 파생식, 서비스 필터, 날짜 기준을 함께 확인한다.

특히 운영 AQPR을 읽을 때 `aqpr` 또는 `frequency`라는 Header 하나만 선택하지 않는다. 같은 필터의 유효 견적수와 대상 Request 수로 재계산하고 Source Query 정의와 일치하는지 검증한다.

Google Sheets의 `IMPORTDATA` 등 외부 데이터 함수는 XLSX Snapshot이나 비Google Engine에서 `#NAME?`으로 보일 수 있다. 이 오류를 원천 데이터 부재로 해석하지 말고 현재 Google Sheet의 계산값과 Source Query 상태를 확인한다. 수식·Import URL에 포함된 API Key나 Token은 절대 인용하거나 저장하지 않는다.

## 시간과 코호트 기준

- 사용자가 다른 시간대를 요청하지 않으면 KST(`UTC + 9`)를 사용한다.
- Cohort 분모는 Lead 또는 Request의 접수 월로 묶는다.
- Cohort 계약 인정은 Deal의 형식상 계약일이 아니라 결제일을 사용한다. Lead가 생성된 Cohort는 유지하고 이후 발생한 결제를 해당 Cohort로 귀속한다.
- Simple 동기간 계약률은 같은 기간의 결제 계약수 / 같은 기간의 신규 Lead 수다. 빠른 현황 지표이지만 진정한 Cohort 지표는 아니다.
- Due date 분석은 이사예정일을 기준으로 운영 수요 쏠림을 본다. Request가 들어온 날짜와 다르다.
- Due date 수요를 접수 수요로 변환할 때 Created date → Due date의 실제 Lead-time 분포를 적용한다. 평균 Lead-time 하나로 모든 수요를 일괄 이동하지 않는다.

## 핵심 테이블과 용도

| 테이블 | 용도와 주의사항 |
|---|---|
| `datamart.rfq_gmv_daily` | 과거 집계·Cohort 분석. 실시간 업데이트 테이블이 아니므로 당일 계약수에 사용하지 않음 |
| `datamart.fct_mv_concierge_bills` | 미소방문 결제·계약 이벤트. 날짜 컬럼을 확인한 뒤 당일 계약수에 우선 사용 |
| `datamart.mv_concierge_wide` | Funnel, 가격, 견적, 파트너 등 MVC 통합 분석. 현재 스키마 확인 필요 |
| `miso_rfq_production_public_request` | Request 단위 운영 원천 |
| `miso_rfq_production_public_quote` | Quote 단위 운영 원천. Submitted 상태만 집계 |
| `datamart.fact_sendbird_messages` | Chat·대화 분석 |
| `datamart.dim_partners` | 파트너 ID·이름·평점과 가능한 경우 Manager·Planner Flag |
| `datamart.fact_requests`, `datamart.fact_quotes` | 공통 Request·Quote Fact. MVC 여부가 명시적이지 않을 수 있으므로 조인 주의 |
| `int_customer_tx` | 과거 리포트 설계에서 약 2025-08까지 사용한 결제 원천 |
| `fact_mv_visit_deals` | 과거 리포트 설계에서 약 2025-09부터 Closed Won과 결제일 로직에 사용. 현재 기준 원천 확인 필요 |

미존재 또는 위험한 가정:

- `datamart.int_mv_concierge_quotes_unnested`는 미존재 오류가 확인되었다. 존재 여부를 다시 확인하기 전 사용하지 않는다.
- `monthly_summary` 같은 CTE 별칭은 실제 Catalog Table이 아니다. 해당 `WITH` 범위 밖에서 참조하면 `TABLE_NOT_FOUND`가 발생할 수 있다.
- Request 테이블에 `service_type` 컬럼이 있다고 가정하지 않는다. 확인된 `service_id` 또는 서비스 Dimension Join을 사용한다.

## 서비스와 상태 판별

- 해당 Source에서 제공한다면 서비스 ID `586`을 MVC 기본 식별값으로 사용한다.
- 공통 Quote Fact에서는 `extras.isMisoVisit` 또는 연결된 Request·RFQ Source로 MVC를 판별할 수 있다. `visit_schedule = 1999-01-01` 같은 특수값은 과거에 사용된 Legacy 구현으로 보고 우선적인 사업 규칙으로 사용하지 않는다.
- 2026-04-17 `Processing`은 플래너와 파트너 `64627`을 제외한 뒤 유효한 파트너 견적 참여가 1개 이상 발생한 상태로 정의되었다.
- 2026-06-21 파트너·태그 오염으로 플래너 식별만으로 Visit Complete를 판별하기 어려워졌다. 스키마 확인 후 `extras.videos`의 `has.video` 같은 유효 영상 증빙을 사용한다.

## 견적 집계 기준

1. Request ID와 Quote ID 또는 실제 Quote Primary Key 기준으로 중복 제거한다.
2. 제출 완료된 견적만 집계한다. `is_submit = TRUE` 또는 현재 스키마의 동등한 조건을 사용한다.
3. 신뢰할 수 있는 Flag·Tag·이름 규칙을 사용해 Miso Manager와 Planner를 제외하고, 필요한 경우 파트너 `64627`도 제외한다.
4. 참여 Slot, 제출 완료, 추천 완료, 고객 노출을 별도 Timestamp·Status로 센다.
5. 고객 노출 견적은 최대 4개지만 파트너 참여·제출은 최대 6개일 수 있다. AQPR에 4개 Clamp를 적용했다면 명시한다.
6. 분모가 전체 Lead, Processing Request, 견적 대상 Request, Visit Complete Request 중 무엇인지 명시한다. 운영 AQPR은 전체 Lead보다 Visit Complete 기준을 우선한다.
7. 견적 6개·4개·3개·2개 제출률은 먼저 Request당 견적수를 집계한 뒤 각 Request 구간을 계산한다. Quote Row를 Request Row로 바로 나누지 않는다.
8. 자동 참여는 확정 견적 입력과 고객 노출이 아니다. 1초견적 Pilot에서는 2시간 내 확정 입력률과 자동 Drop률을 별도로 본다.

## 수요 쏠림 분석

Due date 월별로 다음 순서로 분석한다.

1. Due date별 유니크 Request를 계산한다.
2. Request가 가장 많은 상위 5개 Due date를 선정한다.
3. Top 5 Request 비중, 계약률, AQPR을 계산하고 일반일과 비교한다.
4. 전체 일평균과 Top 5를 제외한 일평균을 모두 유지한다.
5. Top 5 계약률과 Top 5 제외 계약률의 차이를 표시한다.
6. 사용자가 요청한 경우에만 Top 5 계약률이 일반일과 같다는 가정의 Overall Contract Rate를 계산한다.
7. 공급 부족을 진단할 때 Raw Processing Count가 불필요하더라도 월별 Processing 비율을 표시한다.

`estimated_top5_missing_quote_cnt`의 정의:

`Top 5 Visit Complete 수 × Top 5 제외 AQPR - 실제 Top 5 제출 견적수`

Top 5일이 기준 AQPR을 유지하기 위해 추가로 필요했던 제출 견적수로 해석한다. 계산에는 Top 5 Visit Complete 수, 실제 Top 5 Quote 수, 비교 기준 AQPR이 모두 필요하다. 사업적으로 ‘부족분’만 표시한다면 0 미만을 0으로 처리하고, 과잉 공급도 분석한다면 음수 값을 유지한다.

## 수요 구간 분석

수요 구간 분석의 단위는 ‘하루’다. 각 Due date의 Request 수로 일자를 구간화한 뒤, 해당 구간에 속한 날짜들의 Request와 Contract를 합산한다.

미소방문 분석에서 사용한 예시 구간:

- 10~29건, 30~49건, 50~99건, 100~149건, 150~199건, 200~299건, 300~399건, 400건 이상
- 전략 Summary에서는 10~49건, 50~99건처럼 더 넓은 구간을 사용할 수 있음

각 구간에는 최소한 해당 Due date 수, 전체 Request 수, 전체 결제 계약수, 계약률을 표시한다. 손익 모델링에서 계약당 90,000원을 사용하면 실제 AOV가 아니라 가정값이라고 명시한다.

## 계약과 매출 기준

- 당일 계약수는 `datamart.rfq_gmv_daily`가 아니라 `datamart.fct_mv_concierge_bills`의 계약·결제 이벤트를 사용한다.
- 과거 리포트 기준에서는 미소방문 매출로 `commission_amount_6percent`를 사용했다. 현재 상업 정책은 VAT 포함 6.6%로 표현될 수 있다. Source Field 이름은 유지하고 적용 기간과 VAT 처리 기준을 명시적으로 연결한다.
- 과거 데이터를 연결할 때는 2025-08까지 `int_customer_tx`, 2025-09부터 `fact_mv_visit_deals`를 사용한 설계가 있었다. RFQ Transaction의 중복을 제거하고 기준 Paid Timestamp를 확인한다.
- 공헌이익 분석에는 Planner, Operator, Freelancer Planner, 고객획득비용·CPA, 견적 참여비, Benefit·Credit, Cross-sell 중 무엇을 포함했는지 밝힌다.

## 가격 분석 기준

- 확인된 가격 분석 원천은 `datamart.mv_concierge_wide`와 `iceberg.miso_rfq_production_public_quote.extras`의 결합이다.
- 2026-03-02~2026-08-31 Snapshot에는 `basic_moving_price > 0`인 견적 34,186건, 성공 15,005건, 실패 19,181건, 파트너 283곳이 포함되었다. 현재 집계로 재사용하지 않는다.
- House Type은 해당 분석에서 결측 100%였으므로 가격 Grain으로 사용하지 않는다.
- 공통 가격 기준의 제안 Grain은 평수 15·20·25·34·40평 Bucket × 서울·경기·인천이다.
- 기본 가격은 Median을 우선하고 사다리차·엘리베이터·특수작업 등 Add-on은 분리한다. 보관이사는 사용률 약 0.03%로 관찰되어 별도 취급을 검토한다.
- 파트너별 변동계수는 약 16~28%가 관찰되었다. Median ±20~30% Band는 분석 제안이지 배포된 가격 정책이 아니다.

## SQL 작성 점검표

- 1:N Quote·Message Table을 붙이기 전에 Request당 1행인 Base CTE를 만든다.
- Timestamp를 한 번 KST로 변환한 뒤 변환된 값에서 Date와 Month를 파생한다.
- 문자열 Timestamp의 소수점 초 유무가 섞여 있으면 `try_cast`, `try(date_parse(...))`, Source Native Timestamp Cast를 사용한다. `does not match format '%Y-%m-%d %H:%M:%S.%f'` 오류는 소수점 초 형식 혼재로 자주 발생한다.
- Request 지표에는 `count(distinct request_id)`를 사용하고 Event Count는 별도로 정의한다.
- Quote, Payment, Message를 미리 집계해 Join Fan-out을 방지한다.
- 모든 비율과 함께 Raw Numerator·Denominator를 제공해 검증 가능하게 만든다.
- 당일 리포트에는 원천 데이터의 업데이트 지연 여부를 확인하고 명시한다.
- 쿼리 오류가 발생하면 오류 메시지와 확인된 스키마를 기준으로 실제 Table·Column 문제를 수정한다. 추정 컬럼으로 오류를 감추지 않는다.
