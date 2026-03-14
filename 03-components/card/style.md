# Card — Style Spec

> 토큰 매핑, 상태별 스펙, 레이아웃 치수

---

## 1. Anatomy 토큰 슬롯

### variant="base"

| Part | Token Slot |
|------|-----------|
| Container | `background`, `border` (1px), `border-radius`, `elevation` |
| Content Slot | 하위 컴포넌트에 의해 결정 |

### variant="booking"

| Part | Token Slot |
|------|-----------|
| Container | `background`, `border` (1px), `border-radius`, `elevation` |
| Thumbnail | `border-radius`, `width`, `height`, `object-fit` |
| Title | `color`, `typography` |
| Date Range | `color`, `typography` |
| Price | `color`, `typography` |
| Status Badge | `background`, `color`, `typography`, `border-radius`, `padding` |

### variant="listing"

| Part | Token Slot |
|------|-----------|
| Container | `background`, `border` (1px), `border-radius`, `elevation` |
| Image | `border-radius`, `aspect-ratio`, `object-fit` |
| Title | `color`, `typography` |
| Location | `color`, `typography` |
| Rating | `color`, `typography`, `icon-color` |
| Price | `color`, `typography` |
| Feature Tag | `background`, `color`, `typography`, `border-radius`, `padding` |
| Focus Ring | `color` (`$color.stroke.brand`), `offset` (2px), `width` (2px) |

---

## 2. Layout Spec

### variant="base"

| Property | Token | Value |
|----------|-------|-------|
| Padding | `$dimension.spacing.card-padding` | 16px |
| Height | auto | 콘텐츠에 의해 결정 |
| Min Height | — | 제한 없음 |

### variant="booking"

| Property | Token | Value |
|----------|-------|-------|
| Height | auto | 콘텐츠에 의해 결정 |
| Padding | `$dimension.spacing.card-padding` | 16px |
| Thumbnail Size | — | 80 × 80px |
| Thumbnail-Content Gap | `$dimension.x3` | 12px |
| Content Internal Gap | `$dimension.x1` | 4px |
| Badge Padding | `$dimension.x1` / `$dimension.x2` | 4px 8px |

### variant="listing" — Vertical

| Property | Token | Value |
|----------|-------|-------|
| Image Aspect Ratio | — | 16:9 |
| Image-Content Gap | — | 0px (이미지와 콘텐츠 영역이 연속) |
| Content Padding | `$dimension.spacing.card-padding` | 16px |
| Metadata Gap | `$dimension.x2` | 8px |
| Tag Gap | `$dimension.x2` | 8px |

### variant="listing" — Horizontal

| Property | Token | Value |
|----------|-------|-------|
| Image Size | — | 120 × 90px |
| Image-Content Gap | `$dimension.x3` | 12px |
| Content Padding | `$dimension.x3` | 12px |
| Metadata Gap | `$dimension.x1` | 4px |
| Tag Gap | `$dimension.x2` | 8px |

---

## 3. Typography Spec

| Part | Token | Size | Weight |
|------|-------|------|--------|
| Title (listing) | `$typography.title3` | 18px | Bold |
| Title (booking) | `$typography.subtitle2` | 16px | SemiBold |
| Location | `$typography.body2` | 14px | Regular |
| Price | `$typography.price` | 18px | Bold |
| Rating | `$typography.body2-emphasis` | 14px | SemiBold |
| Date Range | `$typography.body2` | 14px | Regular |
| Feature Tag | `$typography.caption1` | 12px | Medium |
| Status Badge | `$typography.caption1` | 12px | Bold |
| Review Count | `$typography.caption1` | 12px | Regular |

---

## 4. Color Spec

### Container

| State | BG | Stroke | Elevation |
|-------|-----|--------|-----------|
| **enabled** | `$color.bg.neutral` | `$color.stroke.neutral` (1px) | `$elevation.low` |
| **hovered** | `$color.bg.neutral-hover` | `$color.stroke.neutral` (1px) | `$elevation.medium` |
| **pressed** | `$color.bg.neutral-pressed` | `$color.stroke.neutral` (1px) | `$elevation.low` |
| **focused** | `$color.bg.neutral` | `$color.stroke.brand` (ring) | `$elevation.low` |
| **selected** | `$color.bg.neutral` | `$color.stroke.brand` (2px) | `$elevation.low` |

### Text Colors

| Part | Token |
|------|-------|
| Title | `$color.fg.neutral` |
| Location | `$color.fg.neutral-weak` |
| Price | `$color.fg.neutral` |
| Rating Text | `$color.fg.neutral` |
| Rating Star (filled) | `$color.fg.warning` |
| Rating Star (empty) | `$color.fg.disabled` |
| Date Range | `$color.fg.neutral-weak` |
| Feature Tag Text | `$color.fg.neutral` |
| Feature Tag BG | `$color.bg.neutral-weak` |

### Status Badge (booking)

| Status | BG | Text |
|--------|-----|------|
| **확정** (confirmed) | `$color.bg.positive` | `$color.fg.on-brand` |
| **대기** (pending) | `$color.bg.warning-weak` | `$color.fg.warning` |
| **취소** (cancelled) | `$color.bg.critical-weak` | `$color.fg.critical` |

---

## 5. Radius Spec

| Part | Token | Value |
|------|-------|-------|
| Container | `$radius.md` | 12px |
| Image (listing) | `$radius.sm` | 8px (inner radius) |
| Thumbnail (booking) | `$radius.sm` | 8px |
| Status Badge | `$radius.xs` | 4px |
| Feature Tag | `$radius.xs` | 4px |

---

## 6. Elevation Spec

| State | Token | Value |
|-------|-------|-------|
| **enabled** | `$elevation.low` | `0 1px 3px rgba(0,0,0,0.08)` |
| **hovered** | `$elevation.medium` | `0 4px 12px rgba(0,0,0,0.12)` |
| **pressed** | `$elevation.low` | `0 1px 3px rgba(0,0,0,0.08)` |
| **selected** | `$elevation.low` | `0 1px 3px rgba(0,0,0,0.08)` |

---

## 7. Motion Spec

| Transition | Duration | Easing | 속성 |
|-----------|----------|--------|------|
| Hover elevation | `$motion.duration.normal` (250ms) | `$motion.easing.standard` | `box-shadow` |
| Hover background | `$motion.duration.fast` (150ms) | `$motion.easing.standard` | `background-color` |
| 포커스 링 | `$motion.duration.fast` (150ms) | `$motion.easing.standard` | `box-shadow` |
| Selected stroke | `$motion.duration.fast` (150ms) | `$motion.easing.standard` | `border-color`, `border-width` |
| 이미지 로드 | `$motion.duration.normal` (250ms) | `$motion.easing.enter` | `opacity` (0 → 1 fade-in) |

---

## 8. Image Spec

```
Listing (vertical):
- Aspect ratio: 16:9
- object-fit: cover
- border-radius: $radius.sm (8px) — 상단 좌우만 적용 (inner clip)
- placeholder: $color.bg.neutral-weak (로딩 중 배경)

Listing (horizontal):
- Size: 120 × 90px
- object-fit: cover
- border-radius: $radius.sm (8px) — 좌측 상하만 적용 (inner clip)
- placeholder: $color.bg.neutral-weak

Booking (thumbnail):
- Size: 80 × 80px (1:1)
- object-fit: cover
- border-radius: $radius.sm (8px)
- placeholder: $color.bg.neutral-weak
```

---

## 9. Selected State 상세

```
Selected 전환:
1. border-color → $color.stroke.brand (150ms, standard easing)
2. border-width → 2px
3. 내부 padding 1px 감소 (border 두께 보정, 레이아웃 시프트 방지)
4. aria-selected="true"
```
