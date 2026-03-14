# Spacing & Radius

> 4pt 그리드 기반 간격 시스템과 모서리 곡률 토큰

---

## 개요

Carmore의 간격 시스템은 **4px 기본 단위**를 사용합니다. 모든 간격과 크기는 4의 배수로 정의되어 시각적 리듬과 정렬을 보장합니다. 모서리 곡률(Radius)은 요소의 크기와 역할에 따라 체계적으로 적용됩니다.

---

## 1. Base Dimension Scale (기본 치수 스케일)

토큰 형식: `$dimension.x{N}` — 값 = N × 4px

| Scale Token | Value (px) | Value (rem) | 시각 참조 |
|-------------|-----------|-------------|-----------|
| `$dimension.x0.5` | 2 | 0.125 | `▎` |
| `$dimension.x1` | 4 | 0.25 | `▌` |
| `$dimension.x1.5` | 6 | 0.375 | `▊` |
| `$dimension.x2` | 8 | 0.5 | `█` |
| `$dimension.x2.5` | 10 | 0.625 | `█▎` |
| `$dimension.x3` | 12 | 0.75 | `█▌` |
| `$dimension.x4` | 16 | 1.0 | `██` |
| `$dimension.x5` | 20 | 1.25 | `██▌` |
| `$dimension.x6` | 24 | 1.5 | `███` |
| `$dimension.x8` | 32 | 2.0 | `████` |
| `$dimension.x10` | 40 | 2.5 | `█████` |
| `$dimension.x12` | 48 | 3.0 | `██████` |
| `$dimension.x16` | 64 | 4.0 | `████████` |
| `$dimension.x20` | 80 | 5.0 | `██████████` |

---

## 2. Semantic Spacing Token (시맨틱 간격 토큰)

역할과 용도에 따라 Scale Token을 매핑한 의미론적 간격 토큰입니다.

### 페이지 레벨

| Semantic Token | Scale 참조 | Value | 용도 |
|----------------|-----------|-------|------|
| `$dimension.spacing-x.page-margin` | `x4` | 16px | 모바일 페이지 좌우 여백 |
| `$dimension.spacing-x.page-margin-tablet` | `x6` | 24px | 태블릿 페이지 좌우 여백 |
| `$dimension.spacing-x.page-margin-desktop` | `x8` | 32px | 데스크톱 페이지 좌우 여백 |
| `$dimension.spacing-y.page-top` | `x6` | 24px | 네비게이션 바 아래 여백 |
| `$dimension.spacing-y.page-bottom` | `x16` | 64px | 페이지 하단 여백 (하단 탭 고려) |

### 섹션 레벨

| Semantic Token | Scale 참조 | Value | 용도 |
|----------------|-----------|-------|------|
| `$dimension.spacing-y.section-gap` | `x6` | 24px | 섹션 간 간격 |
| `$dimension.spacing-y.section-gap-large` | `x10` | 40px | 대형 섹션 구분 |
| `$dimension.spacing-y.section-title-to-content` | `x3` | 12px | 섹션 제목과 콘텐츠 사이 |

### 컴포넌트 레벨

| Semantic Token | Scale 참조 | Value | 용도 |
|----------------|-----------|-------|------|
| `$dimension.spacing-y.component-gap` | `x2` | 8px | 관련 요소 간 간격 |
| `$dimension.spacing-y.component-gap-tight` | `x1` | 4px | 밀접한 요소 간 간격 |
| `$dimension.spacing-y.component-gap-wide` | `x4` | 16px | 느슨한 요소 간 간격 |
| `$dimension.spacing.card-padding` | `x4` | 16px | 카드 내부 패딩 |
| `$dimension.spacing.card-padding-compact` | `x3` | 12px | 밀도 높은 카드 패딩 |
| `$dimension.spacing.input-padding-x` | `x3` | 12px | 입력 필드 좌우 패딩 |
| `$dimension.spacing.input-padding-y` | `x2.5` | 10px | 입력 필드 상하 패딩 |
| `$dimension.spacing.button-padding-x` | `x5` | 20px | 버튼 좌우 패딩 |
| `$dimension.spacing.button-gap` | `x2` | 8px | 버튼 내 아이콘-텍스트 간격 |
| `$dimension.spacing.chip-padding-x` | `x3` | 12px | 칩 좌우 패딩 |
| `$dimension.spacing.chip-gap` | `x2` | 8px | 칩 간 간격 |

### 인라인 요소

| Semantic Token | Scale 참조 | Value | 용도 |
|----------------|-----------|-------|------|
| `$dimension.spacing-x.inline-gap` | `x1` | 4px | 아이콘-텍스트 등 인라인 간격 |
| `$dimension.spacing-x.inline-gap-wide` | `x2` | 8px | 넓은 인라인 간격 |
| `$dimension.spacing-y.text-gap` | `x1.5` | 6px | 텍스트 줄 사이 여백 |
| `$dimension.spacing-y.label-to-field` | `x1.5` | 6px | 라벨과 입력 필드 사이 |
| `$dimension.spacing-y.field-to-helper` | `x1` | 4px | 입력 필드와 도움말 사이 |

---

## 3. Radius (모서리 곡률)

| Token | Value (px) | 용도 |
|-------|-----------|------|
| `$radius.none` | 0 | 직각 모서리 (구분선, 이미지 상단 등) |
| `$radius.xs` | 4 | 칩, 태그, 작은 배지 |
| `$radius.sm` | 8 | 버튼, 입력 필드 |
| `$radius.md` | 12 | 카드, 드롭다운 |
| `$radius.lg` | 16 | BottomSheet 상단 모서리 |
| `$radius.xl` | 20 | Dialog |
| `$radius.2xl` | 24 | 대형 모달 |
| `$radius.full` | 9999 | 원형 (아바타, 환약형 배지) |

### 컴포넌트별 Radius 매핑

| 컴포넌트 | Token | Value |
|----------|-------|-------|
| Button (sm/md/lg) | `$radius.sm` | 8px |
| TextField | `$radius.sm` | 8px |
| Card | `$radius.md` | 12px |
| FilterChip | `$radius.full` | 9999px (환약형) |
| BottomSheet (상단) | `$radius.lg` | 16px |
| Dialog | `$radius.xl` | 20px |
| Avatar | `$radius.full` | 9999px (원형) |
| Thumbnail (카드 내) | `$radius.sm` | 8px |

---

## 4. 컴포넌트 높이 (Component Heights)

인터랙티브 요소의 표준 높이입니다.

| Size | Height | 사용 컴포넌트 |
|------|--------|--------------|
| **sm** | 36px (`$dimension.x9`) | Button(sm), FilterChip |
| **md** | 44px (`$dimension.x11`) | Button(md), TextField(md) |
| **lg** | 52px (`$dimension.x13`) | Button(lg), TextField(lg), SearchField |

> 모든 인터랙티브 요소의 최소 터치 타겟: 44×44px (iOS) / 48×48dp (Android)

---

## 5. 그리드 시스템

### 모바일 (< 600px)

```
┌──────────────────────────────────────┐
│←16→┌──────────────────────────┐←16→│
│    │       Content Area       │     │
│    │  Column: 1 (fluid)       │     │
│    └──────────────────────────┘     │
└──────────────────────────────────────┘
  margin: $dimension.spacing-x.page-margin (16px)
  gutter: N/A (single column)
```

### 태블릿 (600px – 1023px)

```
  margin: $dimension.spacing-x.page-margin-tablet (24px)
  columns: 8
  gutter: $dimension.x4 (16px)
```

### 데스크톱 (≥ 1024px)

```
  margin: $dimension.spacing-x.page-margin-desktop (32px)
  columns: 12
  gutter: $dimension.x6 (24px)
  max-width: 1200px (centered)
```

---

## 6. 사용 가이드라인

### DO

- **4px 배수를 사용합니다** — 모든 간격은 `$dimension.x{N}` 토큰을 사용
- **시맨틱 토큰을 우선합니다** — `$dimension.spacing.card-padding` > `$dimension.x4`
- **관련 요소끼리 더 가깝게 배치합니다** (근접성 원칙)
  ```
  제목 ─ 12px ─ 본문 ─ 4px ─ 캡션     (관련 요소: 작은 간격)
        ── 24px ──                      (섹션 구분: 큰 간격)
  ```

### DON'T

- **4px 배수가 아닌 값을 사용하지 않습니다**
  ```
  ❌ margin: 15px;
  ❌ padding: 7px;
  ✅ margin: 16px; ($dimension.x4)
  ✅ padding: 8px; ($dimension.x2)
  ```

- **하드코딩된 픽셀 값을 사용하지 않습니다**
  ```
  ❌ padding: 16px;
  ✅ padding: var(--dimension-x4);
  ```

- **과도한 간격으로 정보 밀도를 낮추지 않습니다**
  - 검색 결과 목록에서는 `component-gap`(8px)으로 밀도 유지
  - 예약 상세 페이지에서는 `section-gap`(24px)으로 가독성 확보

---

## 7. Carmore 도메인 활용 예시

### 검색 결과 리스트

```
┌─────────────────────────────────────────┐
│←16px→ "서울 강남 렌터카"               │ ← page-margin
│                                         │
│  ┌─────────────────────────────────┐   │
│  │  [이미지]     │←12px→ 차량명    │   │ ← card-padding: 16px
│  │  $radius.sm   │       위치      │   │
│  │               │       평점      │   │
│  │               │←──→  가격       │   │ ← component-gap: 8px
│  └─────────────────────────────────┘   │
│  ←─ 8px ─→                             │ ← component-gap (cards)
│  ┌─────────────────────────────────┐   │
│  │  [다음 카드]                     │   │
│  └─────────────────────────────────┘   │
└─────────────────────────────────────────┘
```

### 필터 칩 영역

```
┌──────────────────────────────────────────────┐
│←16→ [차종▾]←8→[가격▾]←8→[연료▾]←8→[더보기] │
│     $chip-gap    $chip-gap   $chip-gap       │
└──────────────────────────────────────────────┘
```
