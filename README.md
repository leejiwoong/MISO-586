# Miso Visit AI Knowledge Pack

미소방문(Moving Concierge, MVC)의 서비스·운영·데이터 기준을 특정 AI 제품에 종속되지 않는 형태로 정리한 공용 지식 팩이다.

## 빠른 사용법

1. AI의 프로젝트 지식 또는 Knowledge 영역에 `core/`와 `schemas/`를 업로드한다.
2. AI의 System Instructions에 `generic/SYSTEM_PROMPT.md`를 넣는다.
3. 질문에 맞는 문서만 우선 검색·참조하도록 설정한다.
4. `오늘`, `현재`, `최신`, 실적 수치 질문은 이 팩의 Snapshot으로 답하지 말고 `core/source-map.md`에 정의된 최신 원본을 조회한다.

## 구성

| 경로 | 역할 |
|---|---|
| `core/` | 사람이 읽는 미소방문 기준 지식과 의사결정 이력 |
| `schemas/metrics.yaml` | KPI 정의, 목표, 분모·제외조건 |
| `schemas/entities.yaml` | 서비스 ID, 핵심 엔터티와 데이터 원천 |
| `schemas/terminology.yaml` | 표준 용어와 표현 규칙 |
| `generic/SYSTEM_PROMPT.md` | 어떤 AI에도 적용 가능한 실행 지침 |
| `examples/acceptance-tests.md` | 답변 품질을 확인하는 대표 테스트 |
| `manifest.yaml` | 버전, 기준일, 로딩 순서, 최신성 정책 |

## 지식 운영 원칙

- `core/`는 미소방문의 기준 지식이며 실시간 데이터베이스가 아니다.
- 날짜가 있는 실적·담당자·지역·정책은 Snapshot으로 취급한다.
- 최신 값은 Sheet, Warehouse, HubSpot, Slack, 공식 문서에서 확인한다.
- 사실, 목표, 제안, 가정, 과거 Snapshot을 섞지 않는다.
- 숫자에는 분석 단위, 날짜 기준, 시간대, 분자·분모, 제외조건, 중복 제거 기준을 붙인다.
- 고객 개인정보와 Credential은 저장·출력하지 않는다.

## 권장 로딩 순서

1. `generic/SYSTEM_PROMPT.md`
2. `manifest.yaml`
3. 질문과 직접 관련된 `core/` 문서
4. 계산 또는 자동화가 필요할 때 관련 `schemas/` 파일

전체 A-Z 온보딩 요청에만 모든 `core/` 문서를 함께 사용한다. 일반 질문에서 전 문서를 매번 넣으면 비용이 커지고 오래된 Snapshot이 과도하게 영향을 줄 수 있다.

## 배포 범위

이 버전은 1단계 공용 Knowledge Pack이다. ChatGPT, Claude, Gemini, Cursor, Replit 등 제품별 전용 Adapter와 Live Data Connector는 포함하지 않는다. 각 제품에는 위 빠른 사용법으로 적용할 수 있다.

## 버전 관리

- 현재 버전: `1.0.0`
- 지식 기준일: `2026-09-12`
- 중요한 정책·스키마 변경 시 `manifest.yaml`의 버전과 기준일을 함께 갱신한다.
- 최근 수치만 바뀐 경우 Snapshot 문서에 기준일을 명시하고 기존 이력을 삭제하지 않는다.

