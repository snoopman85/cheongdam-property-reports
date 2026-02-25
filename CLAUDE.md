# 부동산 매물 모바일 보고서 생성기

## 프로젝트 목적
CSV 매물 데이터를 읽어 카카오톡 공유용 모바일 원페이지 HTML 보고서를 자동 생성한다.
Claude Code → GitHub → Vercel 배포 파이프라인.

## 데이터
- 소스: `data/properties.csv` (네이버 부동산 수집)
- 지역: 서울 강남구 청담동
- 유형: 빌딩/상가 통임대 (월세)
- 컬럼(21개): 고유번호, 지번주소, 도로명주소, 거래유형, 보증금, 월세, 매매가, 연면적, 대지면적, 매물명, 건물용도, 지상층수, 지하층수, 주차대수, 준공일, 매물특징, 상세설명, 공인중개사, 이미지수, URL, 수집일시

## 출력 규칙
- 파일: `public/{고유번호}-{slug}.html`
- 단일 HTML (외부 의존성 없음, Tailwind CDN만 허용)
- UTF-8 인코딩
- 모바일 퍼스트 (375px 기준, max-width 100%)

## 디자인 규칙
- Tailwind CSS v3 CDN
- 한글 폰트: Pretendard (CDN)
- 메인 색상: #2563EB (파랑), 배경: #F8FAFC
- 카카오톡 OG 메타태그 필수 (og:title, og:description, og:image)
- CTA 버튼: 전화 문의 (tel: 링크), 네이버 매물 보기 (원본 URL)

## 워크플로우
1. data-parser: CSV 행 → 정제 JSON
2. copywriter: 상세설명에서 광고 제거 → 마케팅 카피
3. html-builder: 템플릿 + 데이터 + 카피 → HTML
4. qa-checker: 검증 (PASS/FAIL)

## 명령어
- `/generate-report {고유번호}` — 단건 보고서 생성
- `/generate-all` — 전체 매물 일괄 생성
- `/deploy` — git push → Vercel 자동 배포
