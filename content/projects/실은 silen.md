---
type: project
id: silen
title: 실은 (silen)
oneliner: 똑같다고 생각한 하루에서 놓친 차이를 찾아주는 앱
period_start: 2026-07-22
period_end: 2026-07-29
duration: 1주
context: "[[개인 프로젝트]]"
team_size: 1
my_role: 1인 전담 — DB·인증·백엔드·워커·LLM·프론트 전 영역
my_commits: 287
my_prs: 9
award: null
stack: ["[[Next.js]]", "[[TypeScript]]", "[[Python]]", "[[PostgreSQL]]", "[[pgmq]]", "[[Vertex AI]]", "[[Supabase]]"]
tags: [AI, LLM, 백엔드, 데이터파이프라인, 프라이버시, eval, 1인개발]
repo: https://github.com/seongwwww/silen
featured: true
status: 개발중단
---

# 실은 (silen)

> 똑같다고 생각한 하루에서 놓친 차이를 찾아주는 앱. **"실은 아무것도 아니지 않았다."**

1인 개발 · **커밋 287개 · PR 9건** · 1주

---

## 💡 아이디어

매일이 똑같다고 느끼지만 실제로는 다르다. 그 차이를 사람이 직접 찾기는 어렵다.
그래서 **5초 기록**만 남기면 시스템이 대신 차이를 찾아 알려주는 앱.

제품 원칙에 그 태도가 박혀 있다:

> **"의무가 아니라 선물."** 스트릭·연속 기록 압박 등 죄책감 유도 UI 금지. 평범한 날은 평범하게.
> **"과잉해석 금지."** 자기계발 앱화 금지. 이미 있었던 작은 변화를 발견해줄 뿐.

❓ 이 아이디어가 어디서 나왔나 — 본인 경험?

## 🔍 도출 과정 — PR 순서가 곧 아키텍처

혼자 만들었지만 **9개의 PR로 레이어를 쪼개서** 쌓았다.

| # | PR | 무엇 |
|---|---|---|
| 1 | 스캐폴딩 | 2자산 부팅 · 테스트 하네스 · 로컬 DB |
| 2 | ADR-0002 스키마 | 근거 조인 테이블 · **deletion ledger** |
| 3 | auth | 익명 시작 · 매직링크 · **RLS 정책** |
| 4 | 기록 백엔드 | 텍스트 · 감정 · 사진 쓰기 경로 |
| 5 | 워커 파이프라인 | **pgmq + 트리거 + 소비** |
| 6 | 엔티티 추출 | Vertex Gemini · **가드레일 · eval** |
| 7 | 엔티티 통계 차이 검출 | detector |
| 8 | 차이 서술 | LLM narration · 가드레일 · eval |
| 9 | 질문 세션 | 이어 쓰기 UI |

**설계서를 먼저 쓰고 구현했다.** `docs/superpowers/specs/2026-07-23-worker-pipeline-design.md`와 `plans/`에 기능별 설계서·실행 계획이 남아 있다.

## 🧱 어려웠던 것

❓ 1주 만에 287커밋을 낸 방식에서 가장 힘들었던 것은?
❓ 왜 개발을 멈췄나 (배포까지 안 간 이유)

## ⚖️ 설계 결정과 근거

### 탐지=통계, 서술=LLM

`.claude/rules/ai-evals.md` 첫 줄 — **"핵심: 탐지=통계, 서술=LLM."**
강제 사항: *"차이 탐지 결과는 deterministic detector에서만 생성. LLM을 탐지에 쓰지 않는다."*

이유 세 갈래:
1. **회귀 테스트가 CI 게이트라서** — *"골든셋 통과가 CI 게이트", "false positive 회귀 차단"*. 탐지가 비결정적이면 골든셋이 무의미
2. **비용** — *"탐지는 통계로(무료). LLM은 lazy 서술 호출에만. 필터·게이트는 소형 모델."*
3. **환각 차단** — *"근거 없는 문장 비율 0% 목표", "통계에 없는 인과(`~때문에`) 혼입 0"*

### surprisal 구현에 들어간 판단

`worker/src/silen_worker/detection/surprisal.py`:

- **활성 기록일 기준** — 달력 경과일이 아니라 "실제 기록이 있던 날"만 분모에. 기록 건너뛴 날이 불리하게 작용하지 않는다 → 제품 원칙 *"의무가 아니라 선물"* 과 일치
- **Jeffreys 평활 `(k+0.5)/(n+1)`** — 확률이 0이나 1로 떨어져 `-log2(p)`가 발산하는 걸 막는 안전장치
- **미등장도 놀라움으로 센다** (`bits_absent`) — "늘 있던 게 오늘 없다"도 차이

### `.claude/rules/`를 7종으로 나눈 기준

`CLAUDE.md` 머리말 — **"이 파일은 항상 적용되는 핵심 원칙만 담는다. 세부 규칙은 `.claude/rules/`, 절차는 Skill, 강제 검사는 Hook으로 분리한다. 200줄 이하 유지."**

**컨텍스트 예산을 기준으로 쪼갰다.** 더 근본적으로는 — *"이 저장소는 여러 AI(Claude · Codex · Gemini · Cursor)가 번갈아 작업한다."* 그래서 `AGENTS.md`를 공통 진입점으로, `PROJECT_STATE.md`로 세션 연속성을 확보했다.

### 프라이버시를 스키마 레벨에서

- 기록 **본문을 로그·에러 추적 서비스에 남기지 않는다**
- 센서·사진은 **opt-in, 기본 OFF**
- **파생 신호만 저장** (연속 GPS 대신 방문 장소 라벨)
- **삭제는 DB · Storage · Embedding · 검색 인덱스를 모두 처리** + deletion ledger

### 완료의 정의에 eval을 넣었다

**"완료(DoD) = lint + typecheck + unit + integration + eval 전부 통과."**

## 📸 화면

`app/demo/` 에 데모 페이지와 fixture가 있어 **로컬 실행으로 캡처 가능**하다.

❓ 홈(발견·Daily Wrap) / 5초 기록 화면 / 차이 카드 스크린샷

## 🏅 결과

- eval 스위트 3종 (`diary` · `entities` · `narration`)
- 측정 지표 5종 — 환각율 · 조언혼입율 · 톤불변성 통과율 · 근거정합율 · false positive율
- 배포: 하지 않음

> ⚠️ GitHub 기여 그래프에는 9커밋으로만 잡힌다. 287개 중 **278개가 미등록 이메일(`carmusik2023@gmail.com`)로 작성**됐기 때문. → [[GitHub 이메일 연결 문제]]

## 🔗 연결

[[Next.js]] · [[TypeScript]] · [[Python]] · [[PostgreSQL]] · [[pgmq]] · [[Vertex AI]] · [[Supabase]]
[[탐지는 규칙, 서술은 LLM]] · [[LLM eval과 골든셋]] · [[AI 협업 워크플로우 설계]]

관련: [[정책핏 인천]] — 같은 원칙을 규칙 엔진으로 적용
