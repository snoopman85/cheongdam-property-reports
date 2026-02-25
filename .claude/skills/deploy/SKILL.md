---
name: deploy
description: 생성된 보고서를 GitHub에 push하여 Vercel에 자동 배포합니다
user-invocable: true
disable-model-invocation: true
---

# 배포

생성된 HTML 보고서를 GitHub에 push합니다. Vercel이 자동으로 배포합니다.

## 실행 순서

### Step 1: 상태 확인
```bash
git status
```
변경사항이 없으면 "배포할 변경사항이 없습니다" 출력 후 종료.

### Step 2: 변경사항 스테이징
```bash
git add public/
git add data/properties.csv
```
주의: `.env`, `node_modules`, `data/*.json` (중간 파일)은 제외

### Step 3: 커밋
커밋 메시지 형식: "feat: {변경 요약}"
예: "feat: 매물 003, 004 보고서 생성"
예: "feat: 전체 매물 9건 보고서 일괄 생성"

### Step 4: Push
```bash
git push origin main
```

### Step 5: 배포 확인
사용자에게 Vercel 배포 URL을 안내합니다.
- "GitHub push 완료. Vercel이 자동으로 배포합니다."
- "1~2분 후 확인 가능: https://{project}.vercel.app"
- "개별 매물: https://{project}.vercel.app/{파일명}"
