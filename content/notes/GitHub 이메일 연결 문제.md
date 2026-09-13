---
type: note
---

# GitHub 이메일 연결 문제

## 증상

[[실은 silen]]의 커밋 **287개 중 278개가 GitHub 기여 그래프에 잡히지 않는다.**

```
인정되는 커밋 (13개 repo)  →  s260822@naver.com       ← 계정에 등록됨 ✅
silen 커밋 278개           →  carmusik2023@gmail.com   ← 등록 안 됨 ❌
```

원인은 `C:\workspace\silen`의 로컬 git 설정이 gmail 주소였던 것.

## 해결

GitHub는 커밋을 **이메일로 매칭해 화면에 그릴 때마다** 사용자와 연결한다. 나중에 추가해도 **과거 커밋 전부에 소급 적용**된다.

1. https://github.com/settings/emails
2. Add email address → `carmusik2023@gmail.com`
3. 메일함에서 인증 링크 클릭

> 이 주소는 이미 silen 저장소의 공개 커밋 로그에 노출돼 있다. 등록한다고 새로 공개되는 건 없다.

## 재발 방지

```bash
git config --global user.email "143095110+seongwwww@users.noreply.github.com"
git config --global user.name "seongwwww"
git -C C:/workspace/silen config --unset user.email
```

## 히스토리 재작성은 하지 말 것

`git filter-repo`로 과거 커밋 이메일을 바꾸면 287개 커밋의 SHA가 전부 바뀌고, force push가 필요하고, PR #1~#9의 커밋 링크가 깨진다. 이메일 등록으로 같은 결과를 얻는다.

## 상태

❓ 아직 등록했는지 확인 필요
