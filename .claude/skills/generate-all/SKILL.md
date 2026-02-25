---
name: generate-all
description: CSV의 모든 매물에 대해 보고서를 일괄 생성합니다
user-invocable: true
---

# 전체 매물 보고서 일괄 생성

`data/properties.csv`의 모든 매물에 대해 모바일 HTML 보고서를 생성합니다.

## 실행 순서

### Step 1: CSV 전체 읽기
`data/properties.csv`를 읽어 모든 고유번호 목록을 추출합니다.

### Step 2: 각 매물별 보고서 생성
각 고유번호에 대해 `/generate-report {고유번호}`와 동일한 프로세스를 실행합니다:
1. data-parser → 데이터 파싱
2. copywriter → 카피 작성
3. html-builder → HTML 생성
4. qa-checker → 품질 검증

### Step 3: 목록 페이지 생성
모든 매물 보고서가 생성된 후, `public/index.html` 매물 목록 페이지를 생성합니다.

index.html 구성:
- 헤더: "청담동 매물 보고서"
- 매물 카드 목록 (각 매물별):
  - 매물명 + 주소
  - 보증금/월세
  - 연면적, 층수
  - → 개별 보고서 링크
- 모바일 최적화 (Tailwind CSS)
- 같은 디자인 톤 (파랑 계열)

### Step 4: 결과 요약
생성된 파일 목록과 성공/실패 현황을 보고합니다.

## 완료 시
- 생성된 보고서 수 / 전체 매물 수
- 각 파일 경로 목록
- "/deploy 로 Vercel에 배포할 수 있습니다"
