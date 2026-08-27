# AGENTS.md — 세 번째 커피 대시보드

## 프로젝트 개요
- 단일 파일 정적 대시보드: `index.html` (HTML + CSS + JS 내장)
- 의존성 없음, 빌드 과정 없음, `package.json` 없음
- 브라우저에서 직접 열면 실행됨

## 실행/확인 방법
```bash
# 정적 서버로 띄우기 (권장)
# PowerShell 정적 서버(포트 8765)가 이미 구성되어 있음
# C:\Windows\Temp\helpycode_tcp_serve.ps1 사용

# 또는 단순하게 브라우저로 열기
start index.html
```

## 주요 구조
- `index.html` — 전체 대시보드(헤더, KPI 4개, 월별 매출 차트, 담당자 실적, 제품군 비중)
- 데이터는 스크립트 내 상수(`monthlyData`, `repData`, `productData`)로 하드코딩됨
- Pretendard 폰트 사용(시스템 폰트 폴백 포함)

## 수정 시 주의사항
- 단일 파일이므로 HTML/CSS/JS 섹션을 직접 편집
- 데이터 변경: `<script>` 블록의 상수 배열 수정
- 스타일 변경: `<style>` 블록의 CSS 변수(`--primary-navy` 등) 또는 규칙 수정
- 차트 렌더링 로직: `renderChart()`, `renderRepList()`, `renderProductChart()` 함수 참고

## 팀/발표 정보 (반영 필요 시)
- 팀명: **세 번째 커피**
- 발표 순서: **7번째**
- 발표자: **본인 직접**

## 알려진 제약사항
- Python `http.server` 백그라운드 실행 금지 (포트 8765 좀비 프로세스 이슈)
- 정적 서버 필요 시 PowerShell TcpListener 스크립트 사용