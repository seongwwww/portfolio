---
type: project
id: ai-org-simulation
title: AI Org Simulation
oneliner: PRD를 넣으면 가상 조직이 일해보고 최적 팀 조합을 리포트로 돌려주는 멀티에이전트 시뮬레이터
period_start: 2026-05-22
period_end: 2026-05-23
duration: 2일
context: "[[Google AI Agent Challenge]]"
team_size: 4
my_role: shadow roleplay 에이전트 파이프라인 전체 · SSE 스트리밍 API · 프론트 초기 구현
my_commits: 18
my_prs: 3
award: null
stack: ["[[Python]]", "[[FastAPI]]", "[[Next.js]]", "[[TypeScript]]", "[[Docker]]", "[[Vertex AI]]"]
tags: [AI, 멀티에이전트, PM, 풀스택, 오케스트레이션]
repo: https://github.com/Google-AI-Agent-Challenge-eeeee/ai-org-simulation
featured: true
status: 완료
---

# AI Org Simulation

> PRD와 PM 스타일을 넣으면 **가상 조직이 실제로 일해보고**, 팀 조합을 평가해 리포트로 돌려주는 멀티에이전트 시뮬레이터.

---

## 💡 아이디어

**"이 요구사항에 이 팀 조합이 맞나?"** 는 PM이 늘 하는 판단인데 근거가 경험뿐이다.

PRD를 입력하면 직원·협업 데이터를 바탕으로 팀 조합을 평가하고, 페르소나 시뮬레이션 결과와 정량 평가를 합쳐 리포트를 내는 시스템으로 이 판단을 재현했다.

❓ 팀에서 이 주제를 잡은 계기

## 🔍 도출 과정

### MVP 범위를 자른 기준

README에 명시돼 있다 — 외부 API(GitHub·Slack·Jira·Calendar) 자동 수집은 **현재 미구현**, 대신 `datasets/` 더미 데이터로 엔진을 검증.

> *"이후 API 수집 레이어를 붙여도 상위 파이프라인이 유지되도록 구조화"*

2일 안에 **가치를 만드는 부분(엔진)과 나중에 붙일 부분(수집)을 나눈 판단**이다.

### 판단을 정량화한 순서

`column_selection_draft.py` → `column_weighting_final.py` → `employee_team_ranking.py`

어떤 속성을 볼지 고르고 → 가중치를 정하고 → 팀을 순위화한다. **LLM의 인상 평가가 아니라 가중 점수로 팀 조합을 정했다.** `taxonomy_matcher.py`로 요구사항과 역량을 분류 체계 위에서 맞춘다.

## 🧱 어려웠던 것

❓ 2일 안에 멀티에이전트 파이프라인 전체를 구현하며 막힌 지점
❓ 멀티에이전트 대화가 산으로 갈 때 실제로 겪은 사례

## ⚖️ 설계 결정과 근거

### 에이전트를 프롬프트가 아니라 구조로 통제했다

| 장치 | 역할 |
|---|---|
| `modules/human_confirm.py` + `human_confirm_decision_prd_001.json` | **사람의 확인을 강제하는 체크포인트.** 에이전트가 끝까지 혼자 달리지 못하게 끊음 |
| `pipeline/token_limit_verify.py` | 토큰 초과 사전 검증. 대화가 길어지며 비용·컨텍스트가 터지는 걸 방지 |
| `pipeline/validation_runner.py` · `modules/coverage_check.py` | 단계별 산출물 검증과 누락 점검 |
| `pipeline/section_splitter.py` | PRD를 섹션으로 쪼개 한 번에 다 넣지 않음 |

**"잘 해줘"라고 부탁하는 대신 통과해야 할 관문을 코드로 만들었다.**

### 실시간 스트리밍으로 과정을 보여준다

SSE 엔드포인트로 시뮬레이션 진행 상황을 흘려보내고, 프론트에서 타이핑 효과와 이벤트 마커로 표시. **에이전트가 뭘 하고 있는지 보이게 만든 것**이 신뢰의 근거가 된다.

## 📸 화면

❓ 랜딩 페이지 / 시뮬레이션 진행 화면 / 최종 리포트 스크린샷
- `frontend/public/samples/notification-center-prd.pdf` — 샘플 입력 PRD가 저장소에 있음

## 🏅 결과

수상은 하지 못했다. 남은 것은 2일 만에 만든 **Docker 기반 프론트/백 분리 + CI 워크플로 + Alembic 마이그레이션**을 갖춘 구조.

## 👥 팀과 내 역할

| GitHub | 커밋 |
|---|---|
| coldgeon | 66 |
| **seongwwww (본인)** | **18 · PR 3** |
| HapBok | 4 |
| ssarangkim | 2 |

담당:
- **shadow roleplay 에이전트 파이프라인 전체 (Phase 0–10)** — 핵심 엔진
- PM 페르소나를 roleplay 파이프라인에 연결
- **SSE 실시간 스트리밍 엔드포인트**
- 프론트 SSE 연동 (타이핑 효과 · 이벤트 마커)
- **Next.js 프론트엔드 초기 구현** — 랜딩, 시뮬레이션 UI, Framer Motion 전환
- `api_router` 통합 구조 리팩터링

## 🔗 연결

[[Python]] · [[FastAPI]] · [[Next.js]] · [[TypeScript]] · [[Docker]] · [[Vertex AI]]
[[Google AI Agent Challenge]] · [[멀티에이전트 오케스트레이션]] · [[AI 결과물을 사람이 검토하게 만들기]]

관련: [[US Vibe]] — 같은 멀티에이전트 계열, 운영 규칙 설계 쪽
