# StockPilot

바코드/QR 기반 재고 및 입출고 관리 시스템 (WMS)

## 프로젝트 개요

| 항목 | 내용 |
|------|------|
| **제품명** | StockPilot |
| **대상** | 한국 중소 물류센터, 유통 창고, 제조업 자재관리자 |
| **플랫폼** | 모바일 + 웹 (Flutter, 코드 공유) + 백엔드 API (Spring Boot) |
| **기간** | 30주 (Phase 0 Discovery ~ Phase 3 SaaS) |

## 핵심 기능 (Phase 1 MVP)

| 기능 | 설명 | 사용자 |
|------|------|--------|
| **바코드/QR 스캔** | 스캔 한 번으로 입출고 기록 (30초 이내) | WORKER |
| **실시간 재고 조회** | 대시보드에서 재고 현황 즉시 확인 | MANAGER |
| **CSV/Excel I/O** | 기존 Excel 데이터 이전 비용 $0 | MANAGER |

## 기술 스택

### Phase 1 MVP

```
[Flutter Mobile + Web] ──→ [Cloudflare Tunnel] ──→ [Spring Boot 3.x] ──→ [MySQL 8]
```

| 영역 | 기술 |
|------|------|
| Backend | Spring Boot 3.x, Java 21, Spring Data JPA, Spring Security |
| Frontend | Flutter 3.x (모바일 + 웹 코드 공유), Riverpod, Drift, GoRouter |
| DB | MySQL 8.x |
| 인프라 | Docker Compose, Cloudflare Tunnel |

### Phase 2~3 (측정된 페인 후 도입)

Redis, Kafka, Elasticsearch, Kubernetes, AI 수요예측 등. 모든 도구는 실제 페인이 측정된 후에만 도입.

## Phase 로드맵

```
Phase 0 (W1~W2)    Phase 1 (W3~W6)    Phase 2 (W7~W14)     Phase 3 (W15~W30)
Discovery           MVP                 Pilot                SaaS
인터뷰 5건+         1 paying customer   3~5 customers        10+ customers
가설 검증            wedge 3개           안정화 + 확장         멀티테넌시
```

## 프로젝트 구조

```
wms/
├── CLAUDE.md          # AI 코딩 가이드 (디자인 시스템 참조 규칙)
├── DESIGN.md          # 디자인 시스템 (색상, 폰트, 간격, 미학)
├── README.md
├── .github/           # CI/CD 워크플로
└── wiki/              # 프로젝트 문서 17종
    ├── 01_프로젝트_계획서.md
    ├── 02_ERD_문서.md
    ├── 03_프로젝트_아키텍처_정의서.md
    ├── 04_API_명세서.md
    ├── 05_화면_흐름_시퀀스_다이어그램.md
    ├── 06_화면_기능_정의서.md
    ├── 07_요구사항_정의서.md
    ├── 08_스토리보드.md
    ├── 09_Git_규칙_정의서.md
    ├── 10_환경_설정_템플릿.md
    ├── 11_테스트_전략서.md
    ├── 12_코드_리뷰_규칙.md
    ├── 13_테스트_보고서.md
    ├── 14_배포_가이드.md
    ├── 15_사용자_메뉴얼.md
    ├── 16_운영_메뉴얼.md
    ├── 17_스케줄.md
    └── TODOS.md           # 디자인 + 엔지니어링 리뷰 TODO
```

## 디자인 시스템

| 항목 | 값 |
|------|-----|
| 미학 | Operational/Command Center |
| Primary | `#0B7A3E` (딥 그린) |
| Accent | `#E5790A` (워닝 오렌지) |
| Display 폰트 | General Sans |
| Body 폰트 | Source Sans 3 |
| Data 폰트 | Geist Mono (tabular-nums) |

상세: [DESIGN.md](DESIGN.md)

## API 개요 (Phase 1)

Base URL: `https://api.stockpilot.io`

| Method | Endpoint | 설명 |
|--------|----------|------|
| POST | `/api/v1/auth/signup` | 회원가입 |
| POST | `/api/v1/auth/login` | 로그인 (JWT) |
| GET/POST/PUT/DELETE | `/api/v1/products` | 상품 CRUD |
| POST | `/api/v1/products/import-csv` | CSV 일괄 등록 |
| GET | `/api/v1/inventory` | 재고 조회 |
| POST | `/api/v1/inbound` | 입고 |
| POST | `/api/v1/outbound` | 출고 |

상세: [API 명세서](wiki/04_API_명세서.md)

## 개발 환경 설정

### 사전 요구사항

- Java 21+
- Flutter 3.x
- Docker & Docker Compose
- MySQL 8.x (Docker로 제공)

### 실행

```bash
# 백엔드
docker compose up -d
./gradlew bootRun

# Flutter (모바일)
cd mobile
flutter run

# Flutter (웹)
cd mobile
flutter run -d chrome
```

## 테스트

| 레이어 | 커버리지 목표 | 도구 |
|--------|-------------|------|
| Unit | 전체 60%, 핵심 도메인 90% | JUnit 5, flutter_test |
| Integration | 필수 5개 시나리오 | Testcontainers MySQL |

필수 통합 테스트:
1. 가입 -> 로그인 -> JWT -> 인증된 API 호출
2. 입고: 바코드 조회 -> 수량 -> 재고 증가
3. 출고: 재고 확인 -> 수량 -> 재고 감소 + 부족 시 차단
4. CSV 가져오기: 파일 -> 파싱 -> DB -> 결과
5. 5회 실패 계정 잠금

## 비즈니스 모델

| Tier | 가격 (월) | 대상 |
|------|----------|------|
| Starter | $49 / 창고 | 1인 자영업, 소형 창고 |
| Pro | $199 / 창고 | 중소 물류센터 |
| Enterprise | Custom | 다창고, 복잡 워크플로 |

## 문서

- [프로젝트 계획서](wiki/01_프로젝트_계획서.md)
- [ERD](wiki/02_ERD_문서.md)
- [아키텍처 정의서](wiki/03_프로젝트_아키텍처_정의서.md)
- [API 명세서](wiki/04_API_명세서.md)
- [화면 흐름 / 시퀀스](wiki/05_화면_흐름_시퀀스_다이어그램.md)
- [화면 기능 정의서](wiki/06_화면_기능_정의서.md)
- [요구사항 정의서](wiki/07_요구사항_정의서.md)
- [스토리보드](wiki/08_스토리보드.md)
- [테스트 전략서](wiki/11_테스트_전략서.md)
- [디자인 시스템](DESIGN.md)

## 라이선스

Private
