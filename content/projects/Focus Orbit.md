---
type: project
id: focus-orbit
title: Focus Orbit
oneliner: Mission Log를 분석해 다음 집중·휴식 루틴을 추천하는 적응형 뽀모도로 타이머
period_start: 2026-06-07
period_end: 2026-06-08
context: "[[오픈소스SW 수업]]"
team_size: 4
my_rank: 1
my_role: 3D Galaxy Map UI · 로그 기반 추천 프론트 연동 · 백엔드 테스트 작성 및 빌드 복구
my_commits: 14
my_prs: 6
award: null
stack: ["[[TypeScript]]", "[[Java]]", "[[Docker]]"]
tags: [프론트엔드, 추천, 테스트, 3D]
repo: https://github.com/dlrkawo/OSS-T5
featured: false
---

# Focus Orbit

> Mission Log를 분석해 다음 집중·휴식 루틴을 추천하는 적응형 뽀모도로 타이머

| | |
|---|---|
| 기간 | 2026-06-07 ~ 2026-06-08 |
| 맥락 | [[오픈소스SW 수업]] |
| 팀 | 4명 (기여 1위) |
| 내 기여 | 커밋 14 · PR 6 |
| 저장소 | https://github.com/dlrkawo/OSS-T5 |

---

## 💡 아이디어

> "기존 Pomodoro는 25분 집중 / 5분 휴식 고정 루틴을 쓰지만, 실제 작업과 사용자별 집중 패턴은 모두 다르다."

집중 시간·휴식 시간·완료 여부·중단 여부·일시정지 횟수를 기록해 **다음 미션 루틴을 개인화**한다. 집중 과정을 우주 탐사 Mission으로 표현.

## ⚖️ 설계 결정 — 왜 규칙 기반인가

추천 로직은 **규칙 기반**이다. 학습 모델을 쓰지 않았다.

2일짜리 수업 프로젝트에서 학습 기반을 택했다면 학습 데이터가 없어 동작 자체를 보여줄 수 없다. 규칙 기반은 Mission Log가 쌓이는 즉시 결과가 나온다. **"개인화가 된다"를 시연 가능한 형태로 만드는 것**이 우선이었다.

## 🛠 내가 한 일

FE만 한 게 아니라 **백엔드 테스트까지 손봤다** — `test(api): cover log-based recommendations`, 깨진 백엔드 테스트 컴파일 복구(PR #10).

## 🧱 어려웠던 것

❓ 추천 규칙을 어떤 기준으로 정했나 (예: 중단이 잦으면 집중 시간을 줄인다)

## 📸 화면

❓ 스크린샷

## 🔗 연결

[[TypeScript]] · [[Java]] · [[Docker]]
