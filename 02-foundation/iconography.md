# Iconography

> 아이콘 제작 기준, 크기 체계, 네이밍 규칙

---

## 개요

Carmore의 아이콘 시스템은 렌터카 및 숙박 예약 서비스에서 자주 사용되는 **차량, 숙소, 예약, 탐색** 관련 아이콘을 체계적으로 관리합니다. 일관된 시각 언어를 유지하면서 모든 플랫폼에서 선명하게 렌더링되는 것을 목표로 합니다.

---

## 1. 제작 기준

### 기본 그리드

| 속성 | 값 |
|------|-----|
| 기본 프레임 | 24 × 24px |
| 안전 영역 (Safe zone) | 20 × 20px (상하좌우 2px 여백) |
| 선 굵기 (Stroke) | 2px (기본), 1.5px (디테일) |
| 모서리 곡률 | 직각 또는 2px radius |
| 스타일 | Outlined (기본), Filled (선택됨/활성) |

### 시각 원칙

- **단순함**: 핵심 형태만 남기고 불필요한 디테일 제거
- **일관성**: 모든 아이콘이 같은 굵기, 같은 여백, 같은 곡률을 공유
- **가독성**: 16px까지 축소해도 인식 가능해야 함
- **중립성**: 특정 문화/지역에 편향되지 않는 범용적 형태

---

## 2. 크기 체계

| Token | Size (px) | 용도 |
|-------|-----------|------|
| `$icon.xs` | 16 | 인라인 보조 아이콘 (입력 필드 내, 캡션 옆) |
| `$icon.sm` | 20 | 버튼 내 아이콘, 리스트 아이콘 |
| `$icon.md` | 24 | **기본 크기**, 네비게이션, 액션 바 |
| `$icon.lg` | 32 | 빈 화면(Empty state) 강조, 카테고리 |
| `$icon.xl` | 48 | 빈 화면 중앙 일러스트 보조 |

---

## 3. 색상 적용

아이콘 색상은 Foreground 시맨틱 토큰을 사용합니다.

| 상태 | Color Token |
|------|-------------|
| 기본 | `$color.fg.neutral` |
| 보조 / 비활성 | `$color.fg.neutral-weak` |
| 브랜드 강조 | `$color.fg.brand` |
| 선택됨 / 활성 | `$color.fg.brand` |
| 에러 | `$color.fg.critical` |
| 성공 | `$color.fg.positive` |
| disabled | `$color.fg.disabled` |
| 반전 (어두운 배경 위) | `$color.fg.on-brand` |

---

## 4. 네이밍 규칙

### 형식

```
ic_[category]_[name]_[variant]
```

| 요소 | 설명 | 예시 |
|------|------|------|
| `ic_` | 아이콘 접두사 (필수) | — |
| `[category]` | 기능 카테고리 | `nav`, `action`, `vehicle`, `accom`, `booking`, `status`, `general` |
| `[name]` | 아이콘 이름 (소문자, 언더스코어) | `search`, `car_suv`, `calendar` |
| `[variant]` | 스타일 변형 (선택) | `outlined` (기본, 생략 가능), `filled` |

### 카테고리 분류

| Category | 설명 | 예시 |
|----------|------|------|
| `nav` | 네비게이션 | `ic_nav_back`, `ic_nav_close`, `ic_nav_menu`, `ic_nav_home` |
| `action` | 사용자 액션 | `ic_action_search`, `ic_action_filter`, `ic_action_share`, `ic_action_edit` |
| `vehicle` | 차량 관련 | `ic_vehicle_sedan`, `ic_vehicle_suv`, `ic_vehicle_van`, `ic_vehicle_fuel` |
| `accom` | 숙소 관련 | `ic_accom_hotel`, `ic_accom_villa`, `ic_accom_wifi`, `ic_accom_pool` |
| `booking` | 예약 관련 | `ic_booking_calendar`, `ic_booking_clock`, `ic_booking_receipt`, `ic_booking_cancel` |
| `status` | 상태 표시 | `ic_status_check`, `ic_status_warning`, `ic_status_error`, `ic_status_info` |
| `general` | 범용 | `ic_general_star`, `ic_general_heart`, `ic_general_location`, `ic_general_phone` |

### 예시 목록

```
ic_nav_back                  ← 뒤로가기 화살표
ic_nav_close                 ← X 닫기
ic_action_search             ← 돋보기
ic_action_filter             ← 필터 (슬라이더)
ic_vehicle_sedan             ← 세단 차량
ic_vehicle_suv               ← SUV 차량
ic_accom_hotel               ← 호텔 건물
ic_accom_wifi                ← Wi-Fi 아이콘
ic_booking_calendar          ← 캘린더
ic_booking_receipt           ← 영수증
ic_status_check              ← 체크마크 (성공)
ic_status_check_filled       ← 채워진 체크마크
ic_general_star              ← 별 (평점)
ic_general_star_filled       ← 채워진 별
ic_general_location          ← 위치 핀
ic_general_heart             ← 하트 (찜)
ic_general_heart_filled      ← 채워진 하트
```

---

## 5. 플랫폼별 구현

| 플랫폼 | 형태 | 참조 방식 |
|--------|------|-----------|
| **Figma** | Component (Outlined/Filled variant) | 라이브러리에서 인스턴스 삽입 |
| **Web** | SVG 스프라이트 또는 개별 SVG | `<Icon name="action-search" size="md" />` |
| **iOS** | SF Symbols (표준) + 커스텀 SVG (Carmore 전용) | `UIImage(named: "ic_vehicle_sedan")` |
| **Android** | Vector Drawable (XML) | `@drawable/ic_vehicle_sedan` |

### iOS — SF Symbols 매핑

표준 UI 아이콘은 SF Symbols를 우선 사용하고, Carmore 도메인 전용 아이콘만 커스텀 제작합니다.

| Carmore Icon | SF Symbol 대체 |
|-------------|----------------|
| `ic_nav_back` | `chevron.left` |
| `ic_nav_close` | `xmark` |
| `ic_action_search` | `magnifyingglass` |
| `ic_general_star` | `star` |
| `ic_general_heart` | `heart` |
| `ic_general_location` | `location` |
| `ic_vehicle_sedan` | (커스텀 — SF Symbol 없음) |
| `ic_accom_hotel` | (커스텀 — SF Symbol 없음) |

---

## 6. 사용 가이드라인

### DO

- 의미를 전달할 때 아이콘 + 텍스트 라벨을 함께 사용합니다 (접근성)
- 터치 타겟은 아이콘 크기와 무관하게 최소 44×44px을 확보합니다
- Outlined(기본)과 Filled(활성)를 일관되게 사용하여 상태를 구분합니다

### DON'T

- 아이콘만으로 핵심 정보를 전달하지 않습니다 (색각 이상/스크린 리더 대응)
- 16px 미만으로 축소하지 않습니다
- 아이콘 색상을 임의로 변경하지 않고 시맨틱 토큰을 사용합니다
- 서로 다른 스타일(Outlined + Filled)을 같은 맥락에 혼용하지 않습니다
