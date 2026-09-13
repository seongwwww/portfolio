---
type: project
id: us-vibe
title: US Vibe
oneliner: AI 멀티에이전트 기반 협업 학습 시뮬레이터 — 에이전트 운영 규칙과 모노레포 아키텍처 설계
period_start: 2026-04-09
period_end: 2026-04-12
context: "[[2026 KIT 바이브코딩 공모전]]"
team_size: 4
my_rank: 2
my_role: 모노레포 초기 설계 · 에이전트 운영 계약 정규화 · 팀 역할 차터 · OpenAI API 연동 · 온보딩 API
my_commits: 20
my_prs: 8
award: null
stack: ["[[Next.js]]", "[[NestJS]]", "[[TypeScript]]", "[[OpenAI API]]", "[[Docker]]", "[[GitHub Actions]]"]
tags: [AI, 멀티에이전트, 아키텍처, PM, CI/CD]
repo: https://github.com/US-VIBE/us_vibe
featured: false
---

# US Vibe

> AI 멀티에이전트 기반 협업 학습 시뮬레이터 — 에이전트 운영 규칙과 모노레포 아키텍처 설계

| | |
|---|---|
| 기간 | 2026-04-09 ~ 2026-04-12 |
| 맥락 | [[2026 KIT 바이브코딩 공모전]] |
| 팀 | 4명 (기여 2위) |
| 내 기여 | 커밋 20 · PR 8 |
| 저장소 | https://github.com/US-VIBE/us_vibe |

---

## 💡 아이디어

팀에 들어가 일해보는 경험을 AI 에이전트로 재현한 협업 학습 시뮬레이터.

## 🔍 도출 과정 — 코드보다 문서가 먼저

4일짜리 MVP인데 **PR #2~#6이 전부 문서**다. 코드 PR(`Initialize monorepo`)은 그 다음에 온다.

| PR | 무엇을 먼저 고정했나 |
|---|---|
| #2 | 완료 트리거와 PM/FE 통합 규칙 |
| #3 | 4인 고정 오너십 팀 역할 차터 |
| #4 | 백엔드 단독 MVP 사용자 시나리오 |
| #5 | **비용·실현가능성 통제를 반영한 아키텍처 계획** |
| #6 | 에이전트 정책을 실행 가능한 운영 계약으로 정규화 |

**"비용"을 아키텍처 결정 기준에 넣었고**, 에이전트 지시를 "정책"이 아니라 **실행 가능한 운영 계약(executable operating contracts)** — 즉 지켰는지 판정 가능한 형태로 다시 썼다.

## ⚖️ 설계 결정

4명이 4일 동안 병렬로 붙는 상황에서 **누가 무엇을 책임지는지를 코드보다 먼저 고정**했다. `.ai/` · `.claude/` · `agents/` 디렉터리가 그 산출물.

## 🧱 어려웠던 것

❓ 문서를 먼저 만든 게 실제로 팀 속도에 효과가 있었나
❓ 4일 안에 모노레포+CI+배포까지 밀어붙이며 막힌 지점
❓ 공모전 결과

## 📸 화면

❓ 스크린샷

## 🔗 연결

[[Next.js]] · [[NestJS]] · [[TypeScript]] · [[OpenAI API]] · [[Docker]] · [[GitHub Actions]]
