# 이 폴더는 뭔가요

**이 폴더 자체가 GitHub Pages 저장소입니다.** 파이프라인이 만드는 결과물이 쌓이는
`배포용` 폴더 안에 `.git`이 그대로 들어 있습니다 — 따로 복사해가는 별도 폴더가 없습니다.

## 어떻게 도나

```
손익대시보드_메인\대시보드_결과\배포용\(YY년M월)손익현황_배포용.html   ← 파이프라인이 매달 자동 생성
        │
        │  deploy_copy.py 가 자동 복사 (같은 폴더 안에서)
        ▼
                index.html   ← 지금 이 폴더, 이 파일만 git이 추적
        │
        │  git add / commit / push   (자동 아님 — 사람이 확인 후 직접)
        ▼
GitHub Pages: https://koreatokimec-hub.github.io/mr-dash/
```

`(YY년M월)손익현황_배포용.html` 같은 월별 원본 파일은 `.gitignore`로 제외되어 있어서
git에는 절대 올라가지 않습니다. git이 추적하는 건 `index.html`, `version.json`,
`README.md`, `.gitignore` 4개뿐입니다.

## 평소 쓰는 법

1. `손익대시보드_메인`에서 파이프라인을 돌리면 → 이 폴더의 `index.html`이 자동으로
   최신 내용으로 바뀝니다 (`deploy_copy.py`가 마지막에 실행됨).
2. 필요하면 이 폴더의 `index.html`을 직접 열어 확인합니다.
3. 문제없으면:

```bash
cd "C:\Users\KJS\Desktop\손익대시보드_메인\대시보드_결과\배포용"
git add -A
git commit -m "무엇을 고쳤는지 한 줄"
git push origin main
```

30초~2분 정도 지나면 `https://koreatokimec-hub.github.io/mr-dash/` 에 반영됩니다.

## 뭔가 잘못됐을 때 되돌리는 법

```bash
cd "C:\Users\KJS\Desktop\손익대시보드_메인\대시보드_결과\배포용"
git log --oneline        # 이전 커밋들 확인
git revert HEAD --no-edit   # 방금 올린 것만 취소 (권장 — 이력이 남음)
git push origin main
```

완전히 예전 특정 커밋으로 되돌리고 싶으면(이력을 지우는 방식이라 신중하게):

```bash
git reset --hard <되돌릴 커밋 해시>
git push origin main --force
```

## 접속 암호는 여기 없습니다

암호는 `손익대시보드_메인\배포설정.txt`에서 관리합니다. 이 폴더(공개 저장소로 올라가는 곳)에는
절대 넣지 않습니다.
