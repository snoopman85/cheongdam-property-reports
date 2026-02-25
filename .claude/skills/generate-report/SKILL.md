---
name: generate-report
description: 특정 매물의 모바일 보고서를 생성합니다
user-invocable: true
argument-hint: [고유번호]
---

# 매물 보고서 생성

고유번호 `$ARGUMENTS`에 해당하는 매물의 모바일 HTML 보고서를 생성합니다.

## 실행 순서

### Step 1: 데이터 파싱
data-parser 서브에이전트를 사용하여 `data/properties.csv`에서 고유번호 `$ARGUMENTS` 행을 파싱합니다.
결과: `data/$ARGUMENTS_parsed.json`

### Step 2: 카피 작성
copywriter 서브에이전트를 사용하여 마케팅 카피를 작성합니다.
결과: `data/$ARGUMENTS_content.json`

### Step 3: HTML 생성
html-builder 서브에이전트를 사용하여 `templates/mobile-report.html` 기반으로 최종 HTML을 생성합니다.
결과: `public/{고유번호}-{slug}.html`

### Step 4: 품질 검증
qa-checker 서브에이전트로 생성된 HTML을 검증합니다.
- PASS → 완료 메시지 출력
- FAIL → Step 3를 수정 사항 반영하여 재실행 (최대 2회)

## 완료 시
생성된 파일 경로와 주요 정보를 사용자에게 알려줍니다:
- 파일 경로: `public/{파일명}.html`
- 매물명, 보증금, 월세
- "로컬에서 확인하려면: 브라우저에서 파일을 열어주세요"
- "/deploy 로 Vercel에 배포할 수 있습니다"
