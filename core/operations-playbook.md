# 운영 플레이북

지식 기준일: 2026-09-12. 아래 R&R은 2026-09-12 `Moving_Conciege_Sync`와 운영 Slack의 합의 내용을 반영한다. 담당자 이름은 변동 가능 정보로 취급한다.

## 목차

- 운영 체인과 최신 R&R
- 플래너 Capacity와 배정 운영
- CRM Daily Check와 Sales Call Agent
- 커뮤니케이션, 플래너 교육, 관리 주기

## 운영 체인

| 단계 | 주 담당 | 핵심 산출물 | 관리 지표 |
|---|---|---|---|
| Lead → Appointment | Planner Operations | 확정된 방문 일정 | 연락·배정 완료율 |
| Appointment → Visit Complete | Planner Operations | 완료된 방문과 유효한 영상·정보 | Lead → Visit Complete Rate, 목표 80% |
| Visit Complete → Quote Supply | Partner Operations | 최대 6개 참여, 최대 4개 고객 노출, 추천 완료 | AQPR, 저견적 비율, 6시간 내 제출률, 미추천률 |
| Quotes → Paid Contract | Customer Sales | 고객 선택과 액션 이력 | Visit → Contract, Sales Call 결과 |
| 품질·Capacity | Supervisor | 교육 이수·활동·유지되는 플래너 | 교육, 영상 품질, 현장 정보 누락, 재교육, 활동·유지율 |

## 최신 R&R

2026-09-12 기준 역할 배정 Snapshot:

| 역할 | 관리자 | Backup | 직접 책임 KPI |
|---|---|---|---|
| Planner | 지인호 | 박주희 | Lead → Visit Complete 80% |
| Partner | 유승한 | 석진후 | AQPR 3.8, 견적 2개 이하 비율 0%, 6시간 내 견적 제출 50% |
| Customer Sales | 공석, 임시 석진후 | 유승한 | Lead → Contract 40% |
| Supervisor | 박주희 | — (전담) | Visit Complete 80%, 하위 성과자 계약률 40% 초과, 플래너 평균 계약률 50% |

이는 조직의 영구 정의가 아니라 해당 날짜의 운영 배정이다. 현재 담당자를 묻거나 액션을 할당할 때는 원본 R&R을 다시 확인한다.

### Planner Operations

- Lead → Visit Complete를 책임지고 목표 80%를 관리한다.
- 방문 전 접수 Call, Agent Slack, Manager Chat을 관리한다.
- 방문 일정, 방문 전 취소, No-show, 완료 증빙을 확인한다.

### Partner Operations

- 방문완료 이후의 견적 공급을 책임진다.
- 전략 목표 AQPR은 4.0이며, Daily 운영 기준으로 3.8도 사용되었다. 두 수치를 충돌로 보지 말고 전략 목표와 운영 하한선으로 구분한다.
- 견적 2개 이하 Request 비율을 0%에 가깝게 만든다.
- 방문완료 후 6시간 안에 유효 견적이 제출되는 비율 50%를 운영 목표로 관리한다.
- 견적마다 추천 여부와 고객 노출 가능 여부를 검수한다. 미추천 Request 비율은 0%로 수렴시킨다.
- 견적 제출 알림, 계약 확정 알림, 방문 후 Manager Chat, 수동 매칭, 파트너 온보딩과 리액티브를 관리한다.

### Customer Sales

- Sales Call, CRM Pipeline 관리, 영상 공유와 고객 설명을 담당한다.
- Lead → Contract 40%를 Daily 책임 목표로 관리한다.
- 일반적인 메시지를 반복하기보다 Chat 이력에서 실제 고객의 망설임과 세일즈 포인트를 찾는다.
- 액션 방식별 효과를 분석할 수 있도록 모든 채널과 결과를 기록한다.

### Supervisor

- 영상 교육을 포함한 플래너 교육을 책임진다.
- 교육 이수율, 영상 품질, 현장 정보 누락률, 재교육률, Active Planner 수, Planner 유지율을 관리한다.
- 저성과자 재교육과 Visit Complete → Contract 평균 50% 수준의 플래너 품질을 관리한다.
- 하위 성과자의 계약률이 40%를 넘도록 회복 프로그램을 관리하고 대면·영상 교육 Coverage와 Planner Web 2.0 사용을 확인한다.
- 최신 R&R에서 `Video Shared`는 Ops로 이동했다. Supervisor 업무로 남겨두지 않는다.
- `Ops Product Performance Management`는 최신 R&R 초안에서 제거되었다.

## 플래너 Capacity 기준

- 표준 Capacity: 하루 6건. 동선이 적합한 자차 플래너는 하루 7건.
- 2026-03-03 운영 변경 이후 하루 최대 7건이다.
- 상담 Slot은 2026-03-03부터 30분에서 40분으로 변경되었다.
- 주간·월간 기준은 주 30건, 월 120건이며 월 22일 근무를 가정한다.
- 개인 플래너 근무 기준은 10:00~19:00, 주 5일이다. 확장 계획에서는 고객 방문 가능 시간을 365일 10:00~19:00로 사용할 수 있으므로 서비스 운영 가능 시간과 개인 근무일을 혼동하지 않는다.
- 대중교통 플래너와 자차 플래너를 구분한다. 행정구역별 균등 배분보다 수요 밀도, 실제 이동시간, 버퍼, 취소 위험을 반영한다.

## 배정 운영

- 수동 배정 업무량의 참고값은 1인 하루 50건, 건당 약 7분이다.
- 2026-04-06 하나의 일정 변경 이후 자동배정률이 약 85%에서 약 60%로 낮아진 사례가 있다. 이를 영구적인 기준이 아니라 과거 원인 분석 자료로 사용한다.
- Capacity는 월간 총량만 비교하지 말고 시간대·권역별 예정 방문 수요와 실제 플래너 가용성을 비교한다.

## CRM Daily Check

Pipeline: `100. [MV] Miso Visit Customer`

Internal Pipeline Value: `651633041`

Midday 또는 당일 점검을 별도로 요청하지 않으면 KST 기준 전일 데이터를 점검한다. Summary를 먼저 제시하고 실제 CRM 조치가 필요하거나 원인이 불명확한 건만 Row data로 제공한다.

다음 항목을 점검한다.

1. Funnel별 전체 대상 수
2. 실제 Status 분포
3. CRM 누락 또는 미처리 건
4. 파트너 참여, 제출 완료, 추천 완료, 고객 노출을 분리한 견적 6개·4개·3개·2개·1개·0개별 품질
5. 미추천 Request, 자동 견적의 사람 검수 여부, 방문완료 후 6시간 내 제출 여부
6. Sales Call 1·2·3차 진행과 결과 Status, Closed Won 포함
7. 마감 시점이 지났지만 종결되지 않은 건
8. 조치 대상 Row data의 Due date와 `quotes sent at`
9. Visit Appointment → Visit Complete, 방문 전 취소, No-show, 취소 시점

판단 기준:

- 영상 공유 Funnel에서 `lost`는 정상 종결 상태다. `complete`와 `lost`가 아닌 건을 CRM Check 대상으로 본다.
- `Status 없음`을 그대로 결론으로 사용하지 않는다. 실제 속성값, Pipeline Stage Mapping, Sync 시점을 확인한다.
- 원인이 불명확하면 진단에 필요한 최소 Row data를 제공한다.
- 데이터 기반 Daily Report를 요청받으면 Memo는 기본적으로 제외한다.

## Sales Call Agent 구조

목표 Agent는 HubSpot, Web Chat, Redash·Warehouse Status, 외부 액션 기록을 결합한다.

1. 명확한 Stage와 Due date 기준으로 Sales Call 1·2·3차 대상을 추출한다.
2. Chat 내용을 읽고 고객의 구체적인 망설임, 요구사항, 약속된 후속 조치, 가장 강한 Sales Point를 찾는다.
3. 승인된 범위에서 Chat, Call, SMS, Guide, Script 액션을 제안하거나 실행한다.
4. Channel, Timestamp, Content·Template, Actor, Result, Next Step, Due Time을 기록한다.
5. 최종 결과를 Warehouse·Redash 데이터와 대조한다.
6. Call 차수, Due date 구간, 견적수, 응답, 액션 채널별 계약률을 분석한다.

분석 요청만으로 메시지를 발송하거나 운영 CRM을 변경하지 않는다. 외부 액션은 사용자의 실행 승인과 정확한 대상 확인이 필요하다.

## 커뮤니케이션

- 핵심 운영 Slack Channel은 `#service-moving-visit-ops`다.
- 관련 맥락은 `#service-moving`, `#product-rfq`, `#service-moving-mvos-chat`, `#service-moving-mvos-log`, `#service-moving-alert`에서 확인한다. 단일 채널의 메시지만으로 정책 변경을 확정하지 않는다.
- 과거 운영 시각은 익일 방문 SMS 18:00, 수동 견적 알림 10:00·12:00·18:00이다.
- 일정은 변동 가능하므로 현재 Automation을 확인한 뒤 운영 중이라고 표현한다.
- 고객 메시지는 짧고 고객 상황에 맞춰 작성하며, 견적수·다음 액션·기한·연락 주체를 명확히 한다.

고객 Chat의 반복 이슈는 계약금 취소 후 법인카드 전액 결제, 세금계산서, 견적 수정, 이사일 혼동, 사다리차 정보, 미응답 알림이다. Sales Call 분류와 Script를 만들 때 이 Taxonomy를 우선 사용하되 실제 대화 내용을 확인한다.

## 파트너 안내와 견적 QA

- 2026-09-10 기준 별도 파일형 표준 파트너 가이드는 확인되지 않았다. 지역 확장 SMS와 전화 상담이 주된 안내 방식이었다.
- 파트너에게는 현장 방문 없이 영상·작업 환경·고객 요청 정보를 보고 참여한다는 가치, 기본 참여비 1,000원, VAT 포함 계약 수수료 6.6%를 설명한다. 변동 참여비·프로모션·지역은 발송 전에 최신 정책을 확인한다.
- 최대 6개 업체가 참여할 수 있으나 고객 노출은 최대 4개다.
- 당일 추가금은 원칙적으로 허용하지 않고 예상 변수를 사전에 합의하도록 안내한다. 제출 금액은 최종 견적으로 취급하되 현재 약관과 예외를 확인한다.
- 작은 품목과 불확실한 작업 조건에는 안전 Margin을 반영하고 사람 검수를 유지한다.
- 2026-09-11 처리 중 Request의 약 53%가 추천 견적 없이 보인 사고가 있었다. 원인은 자동 견적 제출의 추천 기준 부재와 미성숙한 품질 로직으로 논의되었다. 영향 건 추천 보완과 이미지 재발송을 즉시 조치했으며, 추천·품질 로직이 안정될 때까지 제한된 자동화 Pilot과 사람 QA를 병행한다.

## 플래너 교육

- 리소스가 많이 드는 대면교육을 온라인 챕터형 교육으로 전환하되, 강사가 직접 설명하는 느낌을 유지한다.
- 선호 형식은 약 10분 단위 Chapter, AI Presenter·Narration, Quiz, 실제 사례다.
- 난도가 높은 Chapter 5는 강사가 Board와 Camera를 번갈아 보며 설명하는 PPT 강의형 Sample로 선정되었다.
- 영상 시청 완료만으로 교육 성과를 판단하지 않는다. 현장 정보 누락, 영상 품질, 견적 가능성, 계약 품질, 재교육률을 함께 측정한다.

## 일일·주간 관리

- Daily: CRM Funnel과 예외, 방문완료 위험, 저견적 Request, Sales Call Backlog, 필요 시 당일 계약수를 확인한다.
- Daily Closing은 Planner의 예정·완료 건수, 완료율, 자동매칭률을 보고한다. Partner는 견적 대상·제출수·AQPR·2개 이하 미소싱 건을, Customer Sales는 기준 Lead·당일 계약·Lead → Contract를 보고한다. 값이 없으면 0으로 추정하지 말고 미보고로 표시한다.
- Weekly Decisions Review: 직전 주와 비교해 신규·변경·번복된 의사결정, 미해결 질문, 담당자, 기한을 정리한다.
- Weekly Expansion Status: 수도권 확장의 Milestone, Launch Readiness, Blocker, Partner Supply, Conversion Signal을 정리한다.
- Daily Market Briefing: 한국 중심의 이사·홈서비스 시장, 경쟁사, 소비자·수요 Trend를 정리한다.

## 시스템·자동화 안전

- 과거 Dashboard Client가 서비스 ID 586 Backoffice Request API를 약 10초마다 Polling해 Server Traffic과 비용을 크게 늘린 사건이 있었다. 해당 Client는 중단되었다.
- 새로운 반복 조회·Dashboard·Agent를 만들기 전 Backend 부하와 비용을 검토하고 담당 팀과 합의한다. 가능하면 Push, Webhook, Queue 또는 낮은 빈도의 집계를 사용한다.
- Slack·Sheet·문서의 URL이나 수식에 포함된 Credential을 로그·리포트·Knowledge Pack에 복사하지 않는다.
