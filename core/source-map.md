# 원본 출처 지도

지식 기준일: 2026-09-12. 이 문서는 미소방문 질문에 어떤 원본을 먼저 확인할지 정한다. 숫자와 담당자는 변동 정보이므로 Snapshot보다 현재 원본을 우선한다.

## 출처 우선순위

| 질문 | 1차 원천 | 보조 원천 | 사용 기준 |
|---|---|---|---|
| 일·주·월 핵심 실적, AQPR, 계약, 매출, GP | Google Sheet `daily number & Moving by Miso Metrics`, 특히 `superset` | 기간별 Metrics View, Warehouse Query | 최신 원본의 계산값·필터·기간을 확인 |
| 운영 R&R, 일일 마감 | `Moving_Conciege_Sync` | `#service-moving-visit-ops` 합의 Thread | 사람 이름은 기준일과 함께 사용 |
| 공식 주간 실적 | `[Moving visit] Weekly Report` | Metrics Sheet | Lead와 Visit Cohort 분모 구분 |
| CRM·Sales Call | HubSpot Pipeline과 속성 | `#service-moving-mvos-chat`, Warehouse | CRM 상태와 실제 Chat·결제 이벤트 대조 |
| 견적 공급·제품 로직 | `#product-rfq`, 제품 문서 | `#service-moving`, 운영 Log | Pilot·배포·수동 운영을 구분 |
| 정책·법률 | 최신 약관·법률 검토 문서 | 운영 안내·Marketing 문구 | 고객 권리에 영향 시 법률 재검토 |
| 지역 확장 | 공식 오픈 문서·제품 설정 | Expansion 문서, Slack | Partner Coverage와 공식 오픈을 구분 |

## 핵심 Google Sheet

문서명: `daily number & Moving by Miso Metrics`

핵심 시트:

- `superset`: 일자·서비스 단위 원천 Import와 핵심 수치. 숫자 질문에서 가장 먼저 확인한다.
- `Moving by Miso Metrics(day)`, `Moving by Miso Metrics(week)`, `Moving by Miso Metrics(month)`: 기간별 표시 View.
- `Know your numbers(MVC)`, `cohort`, `MVC_cohort_rate`: 미소방문 Funnel·Cohort 분석.
- `Month(Daily Contract Rate)`, `Month(Contract Conversion Rate)`: 월별 계약률 View.
- `Excellent Operation`, `daily processing 관리,`: 운영 품질·Processing 관리.
- `Deals(hubspot)`, `Cross sell(hubspot)`: CRM과 Cross-sell 보조 데이터.

`superset`은 외부 Query Import와 Sheet 계산을 포함한다. XLSX Snapshot에서 Google 전용 함수가 `#NAME?`으로 보일 수 있으므로 Snapshot의 재계산 결과만으로 원천 장애를 단정하지 않는다. Header, Source Query, 서비스 필터, 날짜 기준, 파생식을 함께 확인한다. 운영 AQPR은 `aqpr`·`frequency` 같은 Header 이름만 믿지 말고 같은 필터의 유효 견적수 ÷ 대상 Request 수로 검산한다.

## 주요 문서

- `Moving_Conciege_Sync`: 현재 R&R, Daily KPI, 운영 합의
- `[Moving visit] Weekly Report`: 공식 주간 실적과 운영 해석
- `Moving Visit Planner Side`: Planner Funnel, 지역, 방문 Cohort
- `Moving by Miso Review`: P&L, 조직 비용, Cross-sell 전략
- `Moving by Miso - 파트너 성수기 획득·활성화 전략`: Peak Benefit과 Retention 지표
- `Moving by Miso 공통 가격 분석`: 가격 Grain, Median, 변동 Band
- 최신 계약 구조·법률 검토 문서: 고객·파트너·미소의 계약상 역할

## Slack 채널

| 채널 | 용도 |
|---|---|
| `#service-moving-visit-ops` | 핵심 운영, R&R, Daily Closing |
| `#service-moving` | 이사 서비스 공통 운영 |
| `#product-rfq` | 견적 제품, 자동화, Slot·Quote 로직 |
| `#service-moving-mvos-chat` | 고객 Chat과 반복 이슈 |
| `#service-moving-mvos-log` | 시스템·운영 Log |
| `#service-moving-alert` | 운영 Alert |

정책이나 KPI 변경은 한 메시지로 확정하지 않는다. 원문 Thread의 날짜, 결정권자, 후속 문서 반영 여부를 함께 확인한다.

## 최신성 확인 절차

1. 사용자가 `오늘`, `현재`, `최신`을 요청하면 현재 Google Sheet·문서·CRM 원본을 읽는다.
2. 수치는 `daily number & Moving by Miso Metrics`의 `superset`에서 서비스·날짜·필드를 확인한 뒤 목적별 View와 대조한다.
3. R&R과 운영 목표는 `Moving_Conciege_Sync`와 `#service-moving-visit-ops`의 더 최신 합의를 대조한다.
4. 숫자마다 기준일, 시간대, 분모, 상태, 중복 제거, Source를 기록한다.
5. 원본에 접근할 수 없으면 Snapshot 기준임을 밝히고 현재값처럼 표현하지 않는다.

## 보안과 개인정보

- Sheet 수식·Import URL, Slack 메시지, 문서에 포함된 API Key, Token, 비밀번호를 답변·로그·Knowledge Pack에 복사하지 않는다.
- Credential처럼 보이는 값을 발견하면 마스킹하고 소유자에게 삭제·회전을 권고한다.
- 고객 전화번호, 주소, 대화 전문, CRM Row는 업무상 필요한 최소 범위만 사용한다.
