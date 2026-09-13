---
type: note
repo: https://github.com/Capstone-0123/BaseReactProject
---

# BaseReactProject

> [[Nextify]]의 **마이그레이션 결과를 비교·검증하기 위한 기준 프로젝트 모음**

## 왜 중요한가

마이그레이션 도구가 "잘 동작한다"를 주장하려면 **비교 대상**이 있어야 한다.
같은 원본을 세 가지 경로로 옮겨, Nextify의 결과물이 사람이 손으로 한 것·다른 AI 도구가 한 것과 비교해 어떤지 확인한다.

```
원본(netflix-clone3 · React + Vite + TS + Tailwind)
   ├─→ 사람이 직접        →  Manual migration       ← 정답에 가까운 기준선
   ├─→ Cursor AI          →  migrated-by-cursor     ← 경쟁 도구
   └─→ Nextify CLI        →  netflix-clone3-nextified
```

## 벤치마크를 까다롭게 골랐다

원본은 **CSS Modules · 라우팅 · 데이터 패칭 훅 · Tailwind 설정**을 고루 포함한다. Next.js로 넘어갈 때 각각 다른 처리가 필요한 요소들이다.

- `components/` — Navbar · Hero · MovieRow · MovieCard (CSS Modules)
- `pages/Browse.tsx`
- `hooks/useMovies.ts`
- TypeScript 프로젝트 레퍼런스 (`tsconfig.app.json` / `tsconfig.node.json`)

## 의미

[[Nextify]]가 교내 캡스톤 대상과 울산 WAVE 피칭 대회 최우수를 받은 근거가 여기 있어 보인다.
**도구를 만든 것에서 끝나지 않고, 기준선과 경쟁 도구를 놓고 스스로 검증한 구조.**

## 🔗 연결

[[Nextify]] · [[LLM eval과 골든셋]] · [[졸업 캡스톤 디자인]]
