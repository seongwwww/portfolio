---
type: project
id: hello-doctor
title: HelloDoctor
oneliner: 한국에 사는 외국인을 위한 의료 정보 서비스 백엔드
period_start: 2026-01-19
period_end: 2026-02-12
context: "[[UMC]]"
team_size: 2
my_rank: 2
my_role: 약 검색 API · 복약 알람 · 카카오맵 병원 검색 · 다국어 처리
my_commits: 11
my_prs: 5
award: null
stack: ["[[Java]]", "[[Spring Boot]]", "[[MySQL]]", "[[JWT]]", "[[Kakao Map API]]"]
tags: [백엔드, SpringBoot, 외부API, 다국어]
repo: https://github.com/UMC-hello-doctor/HelloDoctor-SB
featured: false
---

# HelloDoctor

> 한국에 사는 외국인을 위한 의료 정보 서비스 백엔드

| | |
|---|---|
| 기간 | 2026-01-19 ~ 2026-02-12 |
| 맥락 | [[UMC]] |
| 팀 | 2명 (기여 2위) |
| 내 기여 | 커밋 11 · PR 5 |
| 저장소 | https://github.com/UMC-hello-doctor/HelloDoctor-SB |

---

## 💡 아이디어

한국에 사는 외국인이 약을 사고 병원을 찾는 일은 언어 때문에 막힌다.

## ⚖️ 설계 결정 — 왜 번역 API인가

**다국어를 번역 API로 처리했다.** (`service/TranslationService.java` + Google API Client 의존성)

메시지 번들이나 DB 다국어 컬럼이 아닌 이유는 데이터 성격에 있다 — **약품 정보와 병원 이름은 외부에서 실시간으로 받아오는 데이터**다. 미리 번역해 둘 수 없으니 런타임 번역이 유일한 선택지다.

## 🛠 구조

- 응답은 `common/ApiResponse`로 통일, 예외는 `GlobalExceptionHandler`에서 일괄 처리
- JWT(`JwtTokenProvider`·`JwtAuthenticationFilter`) + OAuth2 Client 병행
- `util/DistanceUtils.java` — 병원 거리 계산 직접 구현
- SpringDoc OpenAPI로 API 문서 자동화

## 📌 의미

프론트엔드 위주인 이력에서 **백엔드 API를 설계·구현한 증거**.

연관: [HelloDoctor-android](https://github.com/UMC-hello-doctor/HelloDoctor-android) (Kotlin) — 본인 미참여, 백엔드만 담당

## 🧱 어려웠던 것

❓ 번역 API 비용·지연 문제는 없었나

## 📸 화면

❓ 스크린샷

## 🔗 연결

[[Java]] · [[Spring Boot]] · [[MySQL]] · [[JWT]] · [[Kakao Map API]]
