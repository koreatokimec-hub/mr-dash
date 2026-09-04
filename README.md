# 이 폴더는 뭔가요

**`손익대시보드_메인`에서 만든 최종 결과물을 GitHub Pages에 올리기 위한 배포 전용 폴더입니다.**
직접 수정하는 곳이 아닙니다 — 아래 파이프라인이 자동으로 채워 넣습니다.

## 왜 따로 폴더가 있나

```
손익대시보드_메인\대시보드_결과\배포용\(YY년M월)손익현황_배포용.html
        │
        │  deploy_copy.py 가 자동 복사
        ▼
손익대시보드_배포\index.html   ← 지금 이 폴더
        │
        │  git add / commit / push
        ▼
GitHub Pages: https://koreatokimec-hub.github.io/mr-dash/
```

`deploy_copy.py`(작업 폴더 바로 옆에 `손익대시보드_배포`를 만들도록 코드에 정해져 있음)가
매번 여기에 `index.html`·`version.json`을 덮어씁니다. 그래서 이 폴더 자체는 "커밋해서
인터넷에 내보내는 창구" 역할만 합니다 — 실제 작업(코드 수정, 데이터 갱신)은 전부
`손익대시보드_메인`에서 합니다.

## 평소 쓰는 법

`손익대시보드_메인`에서 파이프라인 돌리면(README 참고) 이 폴더의 `index.html`이 자동으로
최신 파일로 바뀝니다. 그 다음 여기서:

```bash
cd "C:\Users\KJS\Desktop\손익대시보드_배포"
git add -A
git commit -m "무엇을 고쳤는지 한 줄"
git push origin main
```

30초~2분 정도 지나면 `https://koreatokimec-hub.github.io/mr-dash/` 에 반영됩니다.

## 뭔가 잘못됐을 때 되돌리는 법

```bash
cd "C:\Users\KJS\Desktop\손익대시보드_배포"
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
