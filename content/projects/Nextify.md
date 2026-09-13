---
type: project
id: nextify
title: Nextify
oneliner: React 프로젝트를 Next.js로 옮겨주는 마이그레이션 자동화 CLI
period_start: 2025-12-01
period_end: 2026-05-24
duration: 6개월
context: "[[졸업 캡스톤 디자인]]"
team_size: 3
my_role: diff 엔진 · VS Code 확장 · Gemini CLI 연동 · 배포
my_commits: 49
my_prs: 18
award: 교내 캡스톤 대상 · 2026 울산 WAVE 대학생 아이디어 피칭 대회 최우수
stack: ["[[Node.js]]", "[[JavaScript]]", "[[VS Code Extension API]]", "[[Gemini]]"]
tags: [AI, CLI, 개발자도구, 배포, 캡스톤, 수상]
repo: https://github.com/Capstone-0123/Nextify
npm: https://www.npmjs.com/package/nextify-cli
npm_downloads: 2215
featured: true
status: 배포중
---

# Nextify

> React 프로젝트를 Next.js로 옮겨주는 **마이그레이션 자동화 CLI**. npm과 VS Code 마켓플레이스에 실제로 배포했다.

🏅 **교내 캡스톤 대상** · 🏅 **2026 울산 WAVE 대학생 아이디어 피칭 대회 최우수**
📦 **npm 누적 다운로드 2,215회** (v0.1.12, MIT)

---

## 💡 아이디어 — 어디서 시작했나

React에서 Next.js로 옮기는 일은 **라우팅·데이터 패칭·훅 사용법이 전부 달라져서** 수작업이 많다. 파일 하나하나 손으로 고치다 보면 뭘 바꿨는지 놓치고, 깨지면 어디서 깨졌는지 모른다.

"이걸 자동화하되, **AI에게 통째로 맡기지는 않는다**"가 출발점이다.

❓ 실제로 이 주제를 잡게 된 계기 — 본인이 마이그레이션을 겪었나, 수업 과제였나?

## 🔍 도출 과정

### 검증 구조를 먼저 만들었다

별도 저장소 [BaseReactProject](https://github.com/Capstone-0123/BaseReactProject)가 있다. 같은 넷플릭스 클론을 **세 가지 경로로 마이그레이션해 비교**한다.

```
원본(netflix-clone3 · React+Vite+TS+Tailwind)
   ├─→ 사람이 직접        →  Manual migration      ← 정답에 가까운 기준선
   ├─→ Cursor AI          →  migrated-by-cursor    ← 경쟁 도구
   └─→ Nextify CLI        →  netflix-clone3-nextified
```

**"잘 동작한다"를 주장하려면 비교 대상이 있어야 한다**는 판단. 수상의 근거가 여기 있어 보인다.

원본은 CSS Modules, 라우팅, 데이터 패칭 훅, Tailwind 설정을 고루 포함한다 — Next.js로 넘어갈 때 각각 다른 처리가 필요한 요소들이다. 벤치마크를 의도적으로 까다롭게 골랐다.

## 🧱 어려웠던 것

❓ 6개월 동안 가장 막혔던 지점은?
❓ "교수님 피드백 정리 전 커밋"이 있는데, 어떤 피드백을 받았고 무엇을 바꿨나?
❓ AI가 바꾼 코드를 사람이 검토하게 만드는 설계에서 가장 어려웠던 점은?

## ⚖️ 설계 결정과 근거

### 마이그레이션을 5단계로 쪼갠 이유

| 단계 | 담당 |
|---|---|
| step1 | 환경 점검 (`step1-env.cjs`) |
| step2 | 레이아웃·프로바이더 생성 |
| step3 | 라우팅 (`route-` · `link-` · `metadata-` · `outlet-migrator`) |
| step4 | 스타일·에셋 (`asset-` · `globalcss-` · `tailwind-styled-migrator`) |
| step5 | 브라우저 API |

**되돌릴 수 있는 단위로 끊었다.** 한 번에 전부 바꾸면 어디서 깨졌는지 알 수 없다. `migrate-next step1 --review`처럼 단계별 리뷰 진입점을 따로 둔 것도 같은 이유.

### AI 결과물을 파일에 바로 쓰지 않는다

CLI가 `.ai-migration/.../session.json`을 남기면 VS Code 확장이 그걸 읽어 Explorer에 **트리·diff·경로 복사 패널**을 띄운다. **세션이라는 중간 상태**를 거치게 한 것이 핵심.

주변 장치도 같은 방향:
- `bin/gemini-health-check.cjs` — 작업 전에 Gemini CLI 사용 가능 여부를 먼저 확인, 없으면 설치까지
- `report/performance-report.cjs` — 변환 결과 리포트
- copy 모드 직후 결과 폴더를 `--add`로 워크스페이스에 자동 추가 (검토 화면까지 가는 마찰 제거)

## 📸 화면

❓ CLI 실행 화면 (`npx nextify-cli --help` 등)
❓ VS Code Nextify Review 패널 diff 화면
❓ 피칭 대회 발표 사진 / 수상 사진

## 🏅 결과

| | |
|---|---|
| 수상 | 교내 캡스톤 **대상**, 2026 울산 WAVE 대학생 아이디어 피칭 대회 **최우수** |
| npm | `nextify-cli` 누적 **2,215 다운로드**, 최신 v0.1.12, MIT |
| 퍼블리셔 | 본인 계정(`seongwwww`) |
| VS Code | 확장 `Nextify Review` 마켓플레이스 배포 |

## 👥 팀과 내 역할

| GitHub | 커밋 |
|---|---|
| coldgeon | 66 |
| **seongwwww (본인)** | **49 · PR 18** |
| hyeryunYou | 36 |

담당: diff 리뷰 시스템(PR #61·#68·#70·#71), Gemini CLI 연동·설치 자동화(#51·#56), **npm + vsix 배포(#54)**, 리포트 양식·패널 디자인

## 🔗 연결

[[Node.js]] · [[JavaScript]] · [[VS Code Extension API]] · [[Gemini]]
[[졸업 캡스톤 디자인]] · [[AI 결과물을 사람이 검토하게 만들기]]

관련: [[BaseReactProject]] — 마이그레이션 A/B 검증 저장소
