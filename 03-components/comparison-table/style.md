# ComparisonTable — Style Spec

> 토큰 매핑, 상태별 스펙, 레이아웃 치수

---

## 1. Anatomy 토큰 슬롯

| Part | Token Slot |
|------|-----------|
| Outer Container | `background`, `border`, `border-radius`, `elevation` |
| Header Cell | `background`, `border` |
| Product Thumbnail | `size`, `border-radius` |
| Product Name | `color`, `typography` |
| Remove Button (✕) | `color`, `size` |
| Feature Label | `color`, `typography` |
| Feature Value | `color`, `typography` |
| Price Value | `color`, `typography` |
| Highlight Cell | `background`, `color` |
| Cell Stroke | `border-color` |

---

## 2. Layout Spec

| Property | Token | Value |
|----------|-------|-------|
| Column Min Width | — | 140px |
| Header Cell Height | — | 120px (썸네일 포함) |
| Row Height | — | 48px |
| Cell Padding | `$dimension.x3` | 12px |
| First Column Width (sticky) | — | 100px |
| Thumbnail Size | — | 64 x 48px |
| Thumbnail Radius | `$radius.sm` | 8px |
| Remove Button Size | — | 24px |
| Remove Button Offset | `$dimension.x2` | 8px (top-right) |
| Table Min Height | — | auto |

> 모바일에서 첫 번째 컬럼(feature label)은 `position: sticky; left: 0`으로 고정됩니다.

---

## 3. Typography Spec

| Part | Token | Size | Weight |
|------|-------|------|--------|
| Product Name | `$typography.subtitle2` (t6Bold) | 15px | Bold |
| Feature Label | `$typography.body2` (t7Regular) | 14px | Regular |
| Feature Value | `$typography.body2-emphasis` (t7Medium) | 14px | Medium |
| Price | `$typography.price` (t5Bold) | 16px | Bold |
| Highlight Badge | `$typography.caption1` (t8Bold) | 12px | Bold |

---

## 4. Color Spec

### Header

| Part | Token | 설명 |
|------|-------|------|
| Header BG | `$color.bg.neutral-weak` | 헤더 행 배경 |
| Product Name | `$color.fg.neutral` | 상품명 텍스트 |
| Remove Button | `$color.fg.neutral-weak` | ✕ 아이콘 기본 |
| Remove Button (hover) | `$color.fg.neutral` | ✕ 아이콘 hover |

### Body Rows

| Part | Token | 설명 |
|------|-------|------|
| Row BG (홀수) | `transparent` | 기본 행 배경 |
| Row BG (짝수) | `$color.bg.neutral-weak` | 교차 행 배경 (zebra stripe) |
| Row Hover BG | `$color.bg.neutral-hover` | Web hover 시 행 배경 |
| Feature Label | `$color.fg.neutral-weak` | 항목명 텍스트 |
| Feature Value | `$color.fg.neutral` | 항목 값 텍스트 |
| Price Value | `$color.fg.neutral` | 가격 텍스트 |
| Cell Stroke | `$color.stroke.neutral-weak` | 셀 구분선 (1px) |

### Highlight (Best Value)

| Part | Token | 설명 |
|------|-------|------|
| Highlight Cell BG | `$color.bg.brand-weak` | 최적 값 셀 배경 |
| Highlight Value | `$color.fg.brand` | 최적 값 텍스트 |
| Highlight Badge BG | `$color.bg.brand` | "최저가" 등 배지 배경 |
| Highlight Badge FG | `$color.fg.on-brand` | 배지 텍스트 |

### Sticky Column

| Part | Token | 설명 |
|------|-------|------|
| Sticky Column BG | `$color.bg.surface` | 스크롤 시 겹침 방지용 불투명 배경 |
| Sticky Column Shadow | `$elevation.low` | 오른쪽 방향 그림자 (스크롤 힌트) |

---

## 5. Radius Spec

| Part | Token | Value |
|------|-------|-------|
| Outer Container | `$radius.md` | 12px |
| Inner Cell | — | 0px (radius 없음) |
| Thumbnail | `$radius.sm` | 8px |
| Highlight Badge | `$radius.full` | 9999px (pill) |

---

## 6. Elevation Spec

| Part | Token | Value |
|------|-------|-------|
| Outer Container | `$elevation.low` | `box-shadow: 0 1px 3px rgba(0,0,0,0.08), 0 1px 2px rgba(0,0,0,0.06)` |
| Sticky Column | `$elevation.low` | 스크롤 시 오른쪽 그림자 표시 |
| Header (sticky) | `$elevation.low` | 스크롤 시 하단 그림자 표시 |

---

## 7. Motion Spec

| Transition | Duration | Easing | 속성 |
|-----------|----------|--------|------|
| 수평 스크롤 | — | momentum (native) | `scroll-position` |
| 컬럼 제거 | `$motion.duration.normal` (250ms) | `$motion.easing.exit` | `opacity`, `width` (collapse) |
| 행 hover | `$motion.duration.fast` (150ms) | `$motion.easing.standard` | `background-color` |
| Highlight 등장 | `$motion.duration.normal` (250ms) | `$motion.easing.enter` | `background-color`, `color` |
| Sticky shadow 등장 | `$motion.duration.fast` (150ms) | `$motion.easing.standard` | `box-shadow` (스크롤 시작 시 표시) |

---

## 8. Responsive Breakpoints

| Breakpoint | 동작 |
|-----------|------|
| Desktop (>= 768px) | side-by-side 전체 테이블 표시, 최대 4컬럼 |
| Mobile (< 768px) | sticky first column + 수평 스크롤, 또는 stacked variant 전환 |

> `variant="stacked"` 모바일에서는 각 상품을 카드 형태로 세로 나열하며, 항목-값을 행으로 표시합니다. Stacked variant의 카드 간 간격은 `$dimension.x3` (12px)입니다.
