# FilterChip — Style Spec

> 토큰 매핑, 상태별 스펙, 레이아웃 치수

---

## 1. Anatomy 토큰 슬롯

| Part | Token Slot |
|------|-----------|
| Container | `background`, `border` (1px), `border-radius` |
| Label | `color`, `typography` |
| Leading Icon | `color`, `size` |
| Trailing Icon (chevron / close) | `color`, `size` |
| Count Badge | `color`, `background`, `typography` |
| Focus Ring | `color` (`$color.stroke.brand`), `offset` (2px), `width` (2px) |

---

## 2. Layout Spec

| Property | Token | Value |
|----------|-------|-------|
| Height | — | 36px |
| Padding X | `$dimension.x3` | 12px |
| Icon-Label Gap | `$dimension.x1` | 4px |
| Chip-to-Chip Gap | `$dimension.x2` | 8px |
| Min Width | — | 48px |
| Icon Size | `$icon.xs` | 16px |
| Count Badge Size | — | 20px (width auto, min-width 20px, height 20px) |
| Count Badge Margin Left | `$dimension.x1` | 4px |

> 칩 그룹 컨테이너는 `overflow-x: auto`, `scroll-snap-type: x mandatory`로 수평 스크롤 구성

---

## 3. Typography Spec

| Part | Token | Size | Weight |
|------|-------|------|--------|
| Label | `$typography.label3` (t7Medium) | 14px | Medium |
| Count Badge | `$typography.caption1` (t8Bold) | 12px | Bold |

---

## 4. Color Spec

### variant="toggle" — unselected

| State | Container BG | Container Stroke | Label | Icon |
|-------|-------------|------------------|-------|------|
| **enabled** | `transparent` | `$color.stroke.neutral` | `$color.fg.neutral` | `$color.fg.neutral` |
| **hovered** | `$color.bg.neutral-hover` | `$color.stroke.neutral` | `$color.fg.neutral` | `$color.fg.neutral` |
| **pressed** | `$color.bg.neutral-pressed` | `$color.stroke.neutral` | `$color.fg.neutral` | `$color.fg.neutral` |
| **focused** | `transparent` | `$color.stroke.brand` (ring) | `$color.fg.neutral` | `$color.fg.neutral` |
| **disabled** | `transparent` | `$color.stroke.disabled` | `$color.fg.disabled` | `$color.fg.disabled` |

### variant="toggle" — selected

| State | Container BG | Container Stroke | Label | Icon |
|-------|-------------|------------------|-------|------|
| **enabled** | `$color.bg.brand-weak` | `$color.stroke.brand` | `$color.fg.brand` | `$color.fg.brand` |
| **hovered** | `$color.bg.brand-weak` | `$color.stroke.brand` | `$color.fg.brand` | `$color.fg.brand` |
| **pressed** | `$color.bg.brand-weak` | `$color.stroke.brand` | `$color.fg.brand` | `$color.fg.brand` |
| **focused** | `$color.bg.brand-weak` | `$color.stroke.brand` (ring) | `$color.fg.brand` | `$color.fg.brand` |
| **disabled** | `transparent` | `$color.stroke.disabled` | `$color.fg.disabled` | `$color.fg.disabled` |

### variant="selection" — unselected

| State | Container BG | Container Stroke | Label | Chevron Icon |
|-------|-------------|------------------|-------|-------------|
| **enabled** | `transparent` | `$color.stroke.neutral` | `$color.fg.neutral` | `$color.fg.neutral` |
| **hovered** | `$color.bg.neutral-hover` | `$color.stroke.neutral` | `$color.fg.neutral` | `$color.fg.neutral` |
| **pressed** | `$color.bg.neutral-pressed` | `$color.stroke.neutral` | `$color.fg.neutral` | `$color.fg.neutral` |
| **focused** | `transparent` | `$color.stroke.brand` (ring) | `$color.fg.neutral` | `$color.fg.neutral` |
| **disabled** | `transparent` | `$color.stroke.disabled` | `$color.fg.disabled` | `$color.fg.disabled` |

### variant="selection" — selected

| State | Container BG | Container Stroke | Label | Chevron Icon | Count Badge BG | Count Badge FG |
|-------|-------------|------------------|-------|-------------|---------------|---------------|
| **enabled** | `$color.bg.brand-weak` | `$color.stroke.brand` | `$color.fg.brand` | `$color.fg.brand` | `$color.bg.brand` | `$color.fg.on-brand` |
| **hovered** | `$color.bg.brand-weak` | `$color.stroke.brand` | `$color.fg.brand` | `$color.fg.brand` | `$color.bg.brand` | `$color.fg.on-brand` |
| **pressed** | `$color.bg.brand-weak` | `$color.stroke.brand` | `$color.fg.brand` | `$color.fg.brand` | `$color.bg.brand` | `$color.fg.on-brand` |
| **disabled** | `transparent` | `$color.stroke.disabled` | `$color.fg.disabled` | `$color.fg.disabled` | `$color.bg.disabled` | `$color.fg.disabled` |

### variant="removable"

| State | Container BG | Container Stroke | Label | Close Icon |
|-------|-------------|------------------|-------|-----------|
| **enabled** | `$color.bg.brand-weak` | `$color.stroke.brand` | `$color.fg.brand` | `$color.fg.brand` |
| **hovered** | `$color.bg.brand-weak` | `$color.stroke.brand` | `$color.fg.brand` | `$color.fg.brand` |
| **pressed** | `$color.bg.brand-weak` | `$color.stroke.brand` | `$color.fg.brand` | `$color.fg.brand` |
| **focused** | `$color.bg.brand-weak` | `$color.stroke.brand` (ring) | `$color.fg.brand` | `$color.fg.brand` |
| **disabled** | `transparent` | `$color.stroke.disabled` | `$color.fg.disabled` | `$color.fg.disabled` |

---

## 5. Radius Spec

| Token | Value |
|-------|-------|
| `$radius.full` | 9999px (pill) |

> 모든 variant, 모든 상태에서 동일한 pill 형태를 유지합니다.

---

## 6. Elevation Spec

| State | Elevation |
|-------|-----------|
| 모든 상태 | `$elevation.none` |

> FilterChip은 평면 요소로, 그림자를 사용하지 않습니다.

---

## 7. Motion Spec

| Transition | Duration | Easing | 속성 |
|-----------|----------|--------|------|
| 토글 전환 | `$motion.duration.fast` (150ms) | `$motion.easing.standard` | `background-color`, `border-color`, `color` |
| 포커스 링 | `$motion.duration.fast` (150ms) | `$motion.easing.standard` | `box-shadow` |
| 제거 애니메이션 | `$motion.duration.fast` (150ms) | `$motion.easing.exit` | `opacity`, `width`, `margin` (collapse) |
| 칩 그룹 스크롤 | — | momentum (native) | `scroll-position` |

---

## 8. Trailing Icon 상세

| Variant | Trailing Icon | 크기 | 설명 |
|---------|--------------|------|------|
| toggle | 없음 | — | trailing icon 없이 라벨만 표시 |
| selection | `chevron-down` | 16px | 드롭다운 존재를 암시 |
| removable | `close` | 16px | 탭 시 칩 제거 |

> selection variant에서 드롭다운이 열린 상태에서는 chevron이 `chevron-up`으로 회전합니다 (`transform: rotate(180deg)`, `$motion.duration.fast`).
