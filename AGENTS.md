# AGENTS.md — 대시보드 저장소

## 프로젝트 개요
이 저장소에는 **단일 파일 정적 대시보드 3개**가 포함되어 있습니다. 의존성 없음, 빌드 과정 없음, `package.json` 없음. 브라우저에서 직접 열면 실행됩니다.

---

## 주요 파일

| 파일 | 설명 | 기술 스택 |
|------|------|-----------|
| `index.html` | **영업 현황 대시보드** — KPI 4개, 월별 매출 차트, 담당자 실적, 제품군 비중 | Vanilla HTML/CSS/JS, Pretendard 폰트 |
| `portfolio.html` | **개발자 포트폴리오** — 히어로, 기술 스택, 프로젝트, 경력, 연락처, 챗봇 | Vanilla HTML/CSS/JS, Pretendard, Leaflet 미사용 |
| `EDU THON/korea-disaster-dashboard.html` | **대한민국 재난 위험 지도** — 시/도/시군구/읍면동 3단계 선택, Leaflet 지도, 위험도 시각화, 대피소 안내 | Leaflet(CDN), Chart.js(CDN), Pretendard(CDN) |
| `EDU THON/eupmyeon_data_for_js.csv` | 읍면동 경계 좌표 데이터 (42개: 종로구 17 + 구미시 25, 실측 lat/lng 포함) | CSV |

---

## 실행/확인 방법

```bash
# 권장: PowerShell 정적 서버 (포트 8765)
# C:\Windows\Temp\helpycode_tcp_serve.ps1 실행 후 브라우저 접속

# 또는 단순하게 브라우저로 열기
start index.html
start portfolio.html
start "EDU THON\korea-disaster-dashboard.html"
```

**서버 접속 URL (정적 서버 실행 시):**
- `http://localhost:8765/index.html` — 영업 현황 대시보드
- `http://localhost:8765/portfolio.html` — 개발자 포트폴리오
- `http://localhost:8765/EDU%20THON/korea-disaster-dashboard.html` — 재난 위험 지도
- `http://localhost:8765/EDU%20THON/eupmyeon_data_for_js.csv` — 읍면동 데이터

---

## 수정 시 주의사항

### 공통
- **단일 파일**이므로 HTML/CSS/JS 섹션을 직접 편집
- 데이터 변경: `<script>` 블록의 상수 배열/객체 수정
- 스타일 변경: `<style>` 블록의 CSS 변수 또는 규칙 수정
- 외부 라이브러리(Leaflet, Chart.js)는 CDN에서 로드 — 인터넷 필요

### `index.html` (영업 현황)
- 차트 렌더링: `renderChart()`, `renderRepList()`, `renderProductChart()`
- 데이터 상수: `monthlyData`, `repData`, `productData`, `TARGET_VALUE`, `MAX_DATA_VALUE`, `MAX_PRODUCT_VALUE`

### `portfolio.html` (포트폴리오)
- 섹션 순서: 히어로 → 기술 스택 → 프로젝트 → 경력+연락처
- 챗봇 설정: `chatbot-config.js` 별도 파일 (Git 무시, API 키 보관용)
- 애니메이션: `IntersectionObserver` 기반 `fadeUp`, `prefers-reduced-motion` 대응

### `EDU THON/korea-disaster-dashboard.html` (재난 위험 지도)
- **3단계 드롭다운**: 시도 → 시군구 → 읍면동 (계층형 의존)
- **지도 경계 표시**:
  - 시군구 선택 시: 해당 시군구의 읍면동들을 **노란 점선 그리드**로 표시 (CSV의 실측 좌표 사용)
  - 읍면동 선택 시: 노란 점선 **숨김**, 선택된 읍면동만 **빨간 실선** 강조 + 해당 위치로 줌인(줌 14)
  - 읍면동 선택 해제 시: 빨간 강조 제거, 시군구 노란 점선 **다시 표시**
- 주요 함수: `showSigunguBounds()`, `showSelectedEupmyeonBounds()`, `clearSigunguBounds()`, `clearSelectedEupmyeonBounds()`, `populateEupmyeonSelect()`, `selectRegion()`
- 데이터 소스: `window.EUPMYEON_DATA` (CSV에서 로드), `ADMIN_DONGS` (서울 샘플), `NATIONWIDE_MOCK_DATA` (전국 주요 시군구)

---

## 알려진 제약사항
- Python `http.server` 백그라운드 실행 금지 (포트 8765 좀비 프로세스 이슈)
- 정적 서버 필요 시 PowerShell TcpListener 스크립트 사용 (`C:\Windows\Temp\helpycode_tcp_serve.ps1`)
- `korea-disaster-dashboard.html`은 Leaflet/Chart.js CDN 로드 필요 — 오프라인에서 지도/차트 미작동
- `portfolio.html`의 챗봇은 `chatbot-config.js`에 API 키 필요 (별도 파일, Git 추적 안 함)

---

## 팀/발표 정보 (필요 시 반영)
- 팀명: **일단만들어조**
- 발표 순서: **25번째**
- 발표자: **본인 직접**