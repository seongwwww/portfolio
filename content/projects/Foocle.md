---
type: project
id: foocle
title: Foocle
oneliner: 가게 사진을 올리면 홍보용 숏폼 영상을 만들어주는 서비스
period_start: 2025-08-11
period_end: 2025-08-20
context: "[[리얼톤(Realthon)]]"
team_size: 2
my_rank: 1
my_role: 메인·마이페이지·가게 상세, 숏폼 생성 API 연동, 토큰 인증, Netlify 배포
my_commits: 32
my_prs: 7
award: null
stack: ["[[React]]", "[[JavaScript]]", "[[styled-components]]", "[[TanStack Query]]", "[[Netlify]]"]
tags: [React, API연동, 인증, 배포, 해커톤]
repo: https://github.com/Foocle/Foocle-FE
featured: false
---

# Foocle

> 가게 사진을 올리면 홍보용 숏폼 영상을 만들어주는 서비스

| | |
|---|---|
| 기간 | 2025-08-11 ~ 2025-08-20 |
| 맥락 | [[리얼톤(Realthon)]] |
| 팀 | 2명 (기여 1위) |
| 내 기여 | 커밋 32 · PR 7 |
| 저장소 | https://github.com/Foocle/Foocle-FE |

---

## 💡 아이디어

가게 사장님이 홍보 영상을 직접 만들기는 어렵다. **사진만 올리면 숏폼이 나오게** 한다.

## 🛠 내가 한 일

- 메인 페이지 전체 구현 (#6)
- 큐레이션 ShopInfo · 가게 상세 · 마이페이지 (#4·#33)
- **숏폼 생성 API 연결** (#32) — 서비스 핵심
- 이미지 업로드 API (#29)
- **AccessToken / RefreshToken 인증** (#25) — 카카오 로그인 콜백 → 토큰 발급 → 만료 시 갱신
- Netlify 배포 및 배포 오류 대응

## 🧱 어려웠던 것

❓ 숏폼 생성은 어떤 기술인가 — AI 영상 생성이면 비중을 크게 올릴 가치가 있음
   (프론트 `createshortform.js`는 백엔드 호출만 해서 코드로는 판별 불가)

## 📸 화면

❓ 스크린샷

## 🔗 연결

[[React]] · [[JavaScript]] · [[styled-components]] · [[TanStack Query]] · [[Netlify]]
