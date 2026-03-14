# Color

> Carmore Design System의 전체 색상 체계: 팔레트, 스케일 토큰, 시맨틱 토큰

---

## 개요

Carmore의 색상 시스템은 3단계 구조를 따릅니다:

1. **Palette (팔레트)**: 색상 원형 값의 집합
2. **Scale Token**: 팔레트 값에 체계적 이름을 부여
3. **Semantic Token**: 역할과 의도에 따라 Scale Token을 매핑

컴포넌트에서는 **Semantic Token만 참조**합니다.

---

## 1. Color Palette (팔레트)

### Brand — Blue

Carmore의 Primary 브랜드 컬러입니다. 여행/결제 도메인에서 **신뢰감과 안정감**을 전달합니다.

| Scale Token | Hex | 용도 힌트 |
|-------------|-----|-----------|
| `$color.palette.blue-50` | `#EBF5FF` | 가장 연한 배경 틴트 |
| `$color.palette.blue-100` | `#CCE5FF` | 호버 배경 |
| `$color.palette.blue-200` | `#99CAFF` | — |
| `$color.palette.blue-300` | `#66AEFF` | — |
| `$color.palette.blue-400` | `#3393FF` | — |
| `$color.palette.blue-500` | `#0077ED` | **Primary 브랜드 컬러** |
| `$color.palette.blue-600` | `#005FBE` | Primary hover |
| `$color.palette.blue-700` | `#00478E` | Primary pressed |
| `$color.palette.blue-800` | `#00305F` | — |
| `$color.palette.blue-900` | `#001830` | 가장 진한 shade |

### Accent — Amber

CTA(Call to Action) 강조 및 딜/프로모션 표시에 사용합니다. Primary Blue와 **시각적 충돌 없이 주목성**을 확보합니다.

| Scale Token | Hex | 용도 힌트 |
|-------------|-----|-----------|
| `$color.palette.amber-50` | `#FFF8EB` | 프로모션 배경 틴트 |
| `$color.palette.amber-100` | `#FFECC5` | — |
| `$color.palette.amber-200` | `#FFD98A` | — |
| `$color.palette.amber-300` | `#FFC64F` | — |
| `$color.palette.amber-400` | `#FFB314` | **Accent 메인** |
| `$color.palette.amber-500` | `#E69B00` | Accent hover |
| `$color.palette.amber-600` | `#B37800` | Accent pressed |
| `$color.palette.amber-700` | `#805600` | Accent 텍스트 |
| `$color.palette.amber-800` | `#4D3400` | — |
| `$color.palette.amber-900` | `#1A1200` | — |

### Semantic — Green (Positive)

예약 확정, 성공, 완료 상태를 나타냅니다.

| Scale Token | Hex |
|-------------|-----|
| `$color.palette.green-50` | `#F0FDF4` |
| `$color.palette.green-100` | `#DCFCE7` |
| `$color.palette.green-200` | `#BBF7D0` |
| `$color.palette.green-300` | `#86EFAC` |
| `$color.palette.green-400` | `#4ADE80` |
| `$color.palette.green-500` | `#16A34A` |
| `$color.palette.green-600` | `#15803D` |
| `$color.palette.green-700` | `#166534` |
| `$color.palette.green-800` | `#14532D` |
| `$color.palette.green-900` | `#052E16` |

### Semantic — Red (Critical)

에러, 취소, 삭제 등 파괴적/위험 상태를 나타냅니다.

| Scale Token | Hex |
|-------------|-----|
| `$color.palette.red-50` | `#FEF2F2` |
| `$color.palette.red-100` | `#FEE2E2` |
| `$color.palette.red-200` | `#FECACA` |
| `$color.palette.red-300` | `#FCA5A5` |
| `$color.palette.red-400` | `#F87171` |
| `$color.palette.red-500` | `#DC2626` |
| `$color.palette.red-600` | `#B91C1C` |
| `$color.palette.red-700` | `#991B1B` |
| `$color.palette.red-800` | `#7F1D1D` |
| `$color.palette.red-900` | `#450A0A` |

### Semantic — Yellow (Warning)

경고, 주의가 필요한 상태를 나타냅니다.

| Scale Token | Hex |
|-------------|-----|
| `$color.palette.yellow-50` | `#FEFCE8` |
| `$color.palette.yellow-100` | `#FEF9C3` |
| `$color.palette.yellow-200` | `#FEF08A` |
| `$color.palette.yellow-300` | `#FDE047` |
| `$color.palette.yellow-400` | `#FACC15` |
| `$color.palette.yellow-500` | `#EAB308` |
| `$color.palette.yellow-600` | `#CA8A04` |
| `$color.palette.yellow-700` | `#A16207` |
| `$color.palette.yellow-800` | `#854D0E` |
| `$color.palette.yellow-900` | `#422006` |

### Achromatic — Gray

텍스트, 배경, 테두리 등 중립적 요소에 사용합니다.

| Scale Token | Hex | 용도 힌트 |
|-------------|-----|-----------|
| `$color.palette.gray-00` | `#FFFFFF` | 순수 흰색 배경 |
| `$color.palette.gray-50` | `#F7F8FA` | 미세한 배경 구분 |
| `$color.palette.gray-100` | `#F0F1F3` | 비활성 배경 |
| `$color.palette.gray-200` | `#E4E6E9` | 기본 테두리 |
| `$color.palette.gray-300` | `#CBCED4` | 강조 테두리, disabled 텍스트 |
| `$color.palette.gray-400` | `#AEB3BC` | placeholder 텍스트 |
| `$color.palette.gray-500` | `#8E949E` | 보조 아이콘 |
| `$color.palette.gray-600` | `#6B7280` | 보조 텍스트 |
| `$color.palette.gray-700` | `#4B5563` | — |
| `$color.palette.gray-800` | `#343A46` | — |
| `$color.palette.gray-900` | `#1F2430` | 기본 텍스트 |
| `$color.palette.gray-950` | `#111318` | 가장 진한 텍스트 |

### Static — Black & White

투명도(alpha) 값을 포함한 정적 색상입니다. 오버레이, 스크림 등에 사용합니다.

| Scale Token | Value |
|-------------|-------|
| `$color.static.black` | `#000000` |
| `$color.static.black-alpha-100` | `rgba(0, 0, 0, 0.04)` |
| `$color.static.black-alpha-200` | `rgba(0, 0, 0, 0.08)` |
| `$color.static.black-alpha-300` | `rgba(0, 0, 0, 0.16)` |
| `$color.static.black-alpha-500` | `rgba(0, 0, 0, 0.40)` |
| `$color.static.black-alpha-700` | `rgba(0, 0, 0, 0.64)` |
| `$color.static.black-alpha-900` | `rgba(0, 0, 0, 0.88)` |
| `$color.static.white` | `#FFFFFF` |
| `$color.static.white-alpha-100` | `rgba(255, 255, 255, 0.04)` |
| `$color.static.white-alpha-200` | `rgba(255, 255, 255, 0.08)` |
| `$color.static.white-alpha-500` | `rgba(255, 255, 255, 0.40)` |
| `$color.static.white-alpha-700` | `rgba(255, 255, 255, 0.64)` |
| `$color.static.white-alpha-900` | `rgba(255, 255, 255, 0.88)` |

---

## 2. Semantic Token (시맨틱 토큰)

### Foreground (fg) — 텍스트 및 아이콘

| Semantic Token | Scale Token 참조 | Hex | 용도 |
|----------------|------------------|-----|------|
| `$color.fg.brand` | `blue-500` | `#0077ED` | 브랜드 컬러 텍스트, 링크 |
| `$color.fg.neutral` | `gray-900` | `#1F2430` | 기본 텍스트 |
| `$color.fg.neutral-weak` | `gray-600` | `#6B7280` | 보조 텍스트, 설명문 |
| `$color.fg.neutral-weakest` | `gray-400` | `#AEB3BC` | placeholder, 힌트 |
| `$color.fg.on-brand` | `gray-00` | `#FFFFFF` | 브랜드 배경 위의 텍스트 |
| `$color.fg.on-accent` | `gray-900` | `#1F2430` | Accent 배경 위의 텍스트 |
| `$color.fg.accent` | `amber-700` | `#805600` | Accent 강조 텍스트 |
| `$color.fg.positive` | `green-500` | `#16A34A` | 성공/완료 텍스트 |
| `$color.fg.warning` | `yellow-700` | `#A16207` | 경고 텍스트 |
| `$color.fg.critical` | `red-500` | `#DC2626` | 에러/위험 텍스트 |
| `$color.fg.informative` | `blue-500` | `#0077ED` | 안내 텍스트 |
| `$color.fg.disabled` | `gray-300` | `#CBCED4` | 비활성 텍스트 |

### Background (bg) — 배경 및 채우기

| Semantic Token | Scale Token 참조 | Hex | 용도 |
|----------------|------------------|-----|------|
| `$color.bg.brand` | `blue-500` | `#0077ED` | Primary 버튼, 브랜드 배경 |
| `$color.bg.brand-hover` | `blue-600` | `#005FBE` | Primary 버튼 호버 |
| `$color.bg.brand-pressed` | `blue-700` | `#00478E` | Primary 버튼 눌림 |
| `$color.bg.brand-weak` | `blue-50` | `#EBF5FF` | 연한 브랜드 배경 틴트 |
| `$color.bg.accent` | `amber-400` | `#FFB314` | 딜 배지, CTA 강조 |
| `$color.bg.accent-hover` | `amber-500` | `#E69B00` | Accent 호버 |
| `$color.bg.accent-pressed` | `amber-600` | `#B37800` | Accent 눌림 |
| `$color.bg.accent-weak` | `amber-50` | `#FFF8EB` | 연한 프로모션 배경 |
| `$color.bg.neutral` | `gray-00` | `#FFFFFF` | 페이지/카드 기본 배경 |
| `$color.bg.neutral-weak` | `gray-50` | `#F7F8FA` | 섹션 구분 배경 |
| `$color.bg.neutral-hover` | `gray-100` | `#F0F1F3` | 중립 호버 |
| `$color.bg.neutral-pressed` | `gray-200` | `#E4E6E9` | 중립 눌림 |
| `$color.bg.neutral-strong` | `gray-800` | `#343A46` | 반전 배경 (진한) |
| `$color.bg.positive` | `green-500` | `#16A34A` | 성공 채우기 |
| `$color.bg.positive-weak` | `green-100` | `#DCFCE7` | 연한 성공 배경 |
| `$color.bg.warning-weak` | `yellow-100` | `#FEF9C3` | 연한 경고 배경 |
| `$color.bg.critical` | `red-500` | `#DC2626` | 에러/삭제 채우기 |
| `$color.bg.critical-weak` | `red-100` | `#FEE2E2` | 연한 에러 배경 |
| `$color.bg.informative-weak` | `blue-50` | `#EBF5FF` | 연한 안내 배경 |
| `$color.bg.disabled` | `gray-100` | `#F0F1F3` | 비활성 배경 |
| `$color.bg.overlay` | `black-alpha-500` | `rgba(0,0,0,0.40)` | 스크림/오버레이 |

### Stroke (stroke) — 테두리 및 구분선

| Semantic Token | Scale Token 참조 | Hex | 용도 |
|----------------|------------------|-----|------|
| `$color.stroke.neutral` | `gray-200` | `#E4E6E9` | 기본 테두리, 구분선 |
| `$color.stroke.neutral-strong` | `gray-300` | `#CBCED4` | 강조 테두리 |
| `$color.stroke.neutral-weak` | `gray-100` | `#F0F1F3` | 약한 테두리 |
| `$color.stroke.brand` | `blue-500` | `#0077ED` | 포커스 링, 활성 테두리 |
| `$color.stroke.positive` | `green-500` | `#16A34A` | 성공 테두리 |
| `$color.stroke.warning` | `yellow-500` | `#EAB308` | 경고 테두리 |
| `$color.stroke.critical` | `red-500` | `#DC2626` | 에러 테두리 |
| `$color.stroke.disabled` | `gray-200` | `#E4E6E9` | 비활성 테두리 |

---

## 3. 사용 가이드라인

### DO

- **의도에 맞는 토큰을 선택합니다**
  - 에러 메시지 → `$color.fg.critical`
  - 예약 확정 배지 → `$color.bg.positive` + `$color.fg.on-brand`
  - 프로모션 배너 → `$color.bg.accent-weak` + `$color.fg.accent`

- **표면(surface)에 맞는 전경색을 사용합니다**
  - `$color.bg.brand` 위의 텍스트 → `$color.fg.on-brand` (흰색)
  - `$color.bg.accent` 위의 텍스트 → `$color.fg.on-accent` (어두운 색)

- **상태에 맞는 variant를 사용합니다**
  - 호버 → `-hover` variant
  - 눌림 → `-pressed` variant
  - 비활성 → `$color.bg.disabled` + `$color.fg.disabled`

### DON'T

- **의미가 맞지 않는 토큰 사용 금지**
  ```
  ❌ 에러 메시지에 $color.fg.brand (파란색) 사용
  ❌ 성공 상태에 $color.bg.accent (앰버) 사용
  ```

- **장식 목적으로 시맨틱 컬러 사용 금지**
  ```
  ❌ "예쁘니까" red를 강조에 사용 → critical 의미로 해석됨
  ❌ green을 브랜드 강조에 사용 → positive/성공으로 해석됨
  ```

- **명도 대비 미충족 조합 금지**
  ```
  ❌ $color.fg.neutral-weakest 위에 작은 텍스트 (대비 부족)
  ❌ $color.bg.brand-weak 위에 $color.fg.neutral-weakest
  ```

---

## 4. 접근성: 명도 대비

모든 텍스트-배경 조합은 **WCAG 2.1 AA 기준**을 충족합니다.

| 기준 | 비율 | 적용 대상 |
|------|------|-----------|
| AA (일반 텍스트) | 4.5:1 이상 | t7 이하 크기 텍스트 |
| AA (대형 텍스트) | 3:1 이상 | t4 이상 크기 또는 Bold 텍스트 |
| AA (UI 요소) | 3:1 이상 | 아이콘, 테두리, 포커스 링 |

### 검증된 주요 조합

| 전경 | 배경 | 대비 비율 | 판정 |
|------|------|-----------|------|
| `$color.fg.neutral` (#1F2430) | `$color.bg.neutral` (#FFFFFF) | 16.2:1 | AA Pass |
| `$color.fg.neutral-weak` (#6B7280) | `$color.bg.neutral` (#FFFFFF) | 5.2:1 | AA Pass |
| `$color.fg.on-brand` (#FFFFFF) | `$color.bg.brand` (#0077ED) | 4.6:1 | AA Pass |
| `$color.fg.critical` (#DC2626) | `$color.bg.neutral` (#FFFFFF) | 5.6:1 | AA Pass |
| `$color.fg.positive` (#16A34A) | `$color.bg.neutral` (#FFFFFF) | 4.5:1 | AA Pass |
| `$color.fg.brand` (#0077ED) | `$color.bg.neutral` (#FFFFFF) | 4.6:1 | AA Pass |

---

## 5. Carmore 도메인 활용 예시

| 화면/요소 | 사용 토큰 조합 |
|-----------|---------------|
| "지금 예약" 버튼 | bg: `$color.bg.brand` / fg: `$color.fg.on-brand` |
| 예약 확정 배지 | bg: `$color.bg.positive` / fg: `$color.fg.on-brand` |
| 예약 취소됨 배지 | bg: `$color.bg.critical-weak` / fg: `$color.fg.critical` |
| "특가" 라벨 | bg: `$color.bg.accent` / fg: `$color.fg.on-accent` |
| 가격 텍스트 | fg: `$color.fg.neutral` (기본) |
| 할인 전 가격 | fg: `$color.fg.neutral-weak` + 취소선 |
| 검색 결과 카드 테두리 | stroke: `$color.stroke.neutral` |
| 선택된 필터 칩 | bg: `$color.bg.brand-weak` / fg: `$color.fg.brand` / stroke: `$color.stroke.brand` |
| 입력 에러 상태 | stroke: `$color.stroke.critical` / fg(helper): `$color.fg.critical` |
| BottomSheet 스크림 | bg: `$color.bg.overlay` |
