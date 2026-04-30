# Design System — StockPilot

## Product Context
- **What this is:** 바코드/QR 기반 재고/입출고 관리 시스템 (WMS)
- **Who it's for:** 한국 중소 물류센터, 유통 창고, 제조업 자재관리자
- **Space/industry:** 창고 관리 소프트웨어 (WMS), 경쟁: Excel(진짜 경쟁자), 박스히어로, 셀러노트
- **Project type:** 대시보드/웹 앱 (React + shadcn/ui) + 모바일 앱 (Flutter + Material 3)
- **Memorable thing:** "이건 진짜 창고용 소프트웨어다" — 전문성과 현장감

## Aesthetic Direction
- **Direction:** Operational/Command Center — 창고 운영 센터의 신뢰감
- **Decoration level:** Minimal — 타이포그래피와 색상이 모든 일을 함. 장식 없음.
- **Mood:** 먼지와 소음 속에서도 정보가 명확하게 전달되는 산업용 기기의 느낌. 차갑고 정밀하지만 적대적이지 않은. 현장 계기판처럼 데이터가 정렬되어 신뢰를 줌.
- **Anti-patterns:** 보라색 그라디언트, 3열 아이콘 그리드, 장식적 blob, 이모지 디자인 요소

## Typography
- **Display/Hero:** General Sans (700, 600) — 넓고 안정적인 산업 소프트웨어의 무게감
- **Body:** Source Sans 3 (400, 500, 600) — 진지하고 가독성 높음. 작은 화면에서도 선명.
- **UI/Labels:** Source Sans 3 (500, 600)
- **Data/Tables:** Geist Mono (400, tabular-nums) — 재고 수량, 금액, SKU가 정렬되어 보이는 모노스페이스
- **Code:** JetBrains Mono
- **Loading:**
  - General Sans: https://api.fontshare.com/v2/css?f[]=general-sans@400,500,600,700&display=swap
  - Source Sans 3: Google Fonts
  - Geist Mono: npm geist 패키지 또는 CDN
- **Scale:**
  - xs: 12px / 0.75rem — 캡션, 뱃지
  - sm: 14px / 0.875rem — 보조 텍스트, 테이블 셀
  - base: 16px / 1rem — 본문
  - lg: 18px / 1.125rem — 강조 본문
  - xl: 20px / 1.25rem — 섹션 제목
  - 2xl: 24px / 1.5rem — 페이지 제목
  - 3xl: 30px / 1.875rem — 히어로 (모바일)
  - 4xl: 36px / 2.25rem — 히어로 (웹)

## Color
- **Approach:** Restrained — 1개 액센트 + 중립색. 색상은 상태와 경고에만 사용.
- **Primary:** #0B7A3E (딥 그린) — 창고/물류의 안전, 정확, 완료. CTA, 활성 상태, 선택됨.
- **Primary Hover:** #096832
- **Primary Light:** #E8F5EE — 배경 하이라이트
- **Accent:** #E5790A (워닝 오렌지) — 저재고, 유통기한 경고 전용. 창고 안전 표지판 색상.
- **Accent Light:** #FEF3E2
- **Neutrals (cool gray):**
  - 50: #F8F9FA (배경)
  - 100: #F1F3F5 (표면)
  - 200: #E9ECEF
  - 300: #DEE2E6 (테두리)
  - 400: #CED4DA
  - 500: #ADB5BD (비활성 텍스트)
  - 600: #6C757D (보조 텍스트)
  - 700: #495057
  - 800: #343A40
  - 900: #1A1D21 (사이드바, 다크 텍스트)
- **Semantic:**
  - Success: #16A34A / light: #DCFCE7
  - Warning: #D97706 / light: #FEF3C7
  - Error: #DC2626 / light: #FEE2E2
  - Info: #2563EB / light: #DBEAFE
- **Dark mode strategy:** 배경 #111317, 표면 #1A1D21, 텍스트 #E9ECEF. Primary 채도 유지, semantic 색상 채도 10% 감소.

## Spacing
- **Base unit:** 4px
- **Density:** Comfortable — 장갑 착용 사용자 고려. 모바일에서 특히 널널한 간격.
- **Scale:**
  - 2xs: 2px
  - xs: 4px
  - sm: 8px
  - md: 16px
  - lg: 24px
  - xl: 32px
  - 2xl: 48px
  - 3xl: 64px
- **Touch targets:** 모바일 최소 48x48px (장갑 착용 고려)

## Layout
- **Approach:** Grid-disciplined — 엄격한 그리드, 예측 가능한 정렬
- **Grid:**
  - Desktop (1024px+): 12 columns, 24px gutter
  - Tablet (768-1023px): 8 columns, 16px gutter, 사이드바 접힘
  - Mobile: single column, 16px padding
- **Max content width:** 1280px
- **Web layout:** 상단바(56px) + 좌측 사이드바(220px) + 컨텐츠 영역
- **Mobile layout:** 상단바(56px) + 컨텐츠 + 하단 탭바(56px, 6개 탭)
- **Border radius:**
  - sm: 4px (뱃지, 작은 요소)
  - md: 8px (카드, 버튼, 입력 필드)
  - lg: 12px (모달, 큰 컨테이너)
  - full: 9999px (pill 뱃지)

## Motion
- **Approach:** Minimal-functional — 상태 변화 알림에만 사용. 장식적 애니메이션 없음.
- **Easing:**
  - enter: ease-out (요소 등장)
  - exit: ease-in (요소 퇴장)
  - move: ease-in-out (위치 변경)
- **Duration:**
  - micro: 50-100ms (토글, 체크박스)
  - short: 150-250ms (토스트 등장, 드롭다운)
  - medium: 250-400ms (모달, 사이드바)
  - long: 400-700ms (페이지 전환)
- **특수 모션:**
  - 바코드 스캔 성공: 햅틱 피드백 + 체크마크 scale(0→1) 200ms
  - 토스트: slide-up + fade-in 200ms, auto-dismiss 2-3초

## Accessibility
- **Color contrast:** 본문 텍스트 4.5:1 이상 (WCAG AA)
- **Touch targets:** 모바일 최소 48x48px
- **Focus indicators:** 모든 인터랙티브 요소에 3px solid primary-light 포커스 링
- **Font size:** 본문 최소 16px

## Decisions Log
| Date | Decision | Rationale |
|------|----------|-----------|
| 2026-04-30 | 초기 디자인 시스템 생성 | /design-consultation 기반. Operational/Command Center 미학, 딥 그린 Primary로 창고 정체성 강화 |
| 2026-04-30 | General Sans + Source Sans 3 선택 | DevPath AI(Satoshi + DM Sans)와 의도적 차별화. 더 넓고 안정적인 산업 소프트웨어 느낌 |
| 2026-04-30 | Geist Mono for data | 재고 수량/금액의 tabular-nums 정렬. "현장 계기판" 느낌 |
| 2026-04-30 | 딥 그린(#0B7A3E) Primary | 대부분 WMS가 파란색 사용. 초록색으로 창고/물류 정체성 차별화 |
| 2026-04-30 | 워닝 오렌지(#E5790A) Accent | 저재고/유통기한 경고 전용. 창고 안전 표지판 연상 |
