# Button — Style Spec

> 토큰 매핑, 상태별 스펙, 레이아웃 치수

---

## 1. Anatomy 토큰 슬롯

| Part | Token Slot |
|------|-----------|
| Container | `background`, `border` (1px), `border-radius`, `elevation` |
| Label | `color`, `typography` |
| Leading/Trailing Icon | `color`, `size` |
| Focus Ring | `color` (`$color.stroke.brand`), `offset` (2px), `width` (2px) |
| Spinner (loading) | `color`, `size` |

---

## 2. Layout Spec

| Size | Height | Padding X | Icon-Label Gap | Icon Size | Min Width |
|------|--------|-----------|---------------|-----------|-----------|
| `sm` | 36px | `$dimension.x3` (12px) | `$dimension.x1` (4px) | `$icon.xs` (16px) | 64px |
| `md` | 44px | `$dimension.x5` (20px) | `$dimension.x2` (8px) | `$icon.sm` (20px) | 80px |
| `lg` | 52px | `$dimension.x6` (24px) | `$dimension.x2` (8px) | `$icon.sm` (20px) | 96px |

> `width="fill"` 시 `width: 100%`, `min-width` 무시

---

## 3. Typography Spec

| Size | Token | Size | Weight |
|------|-------|------|--------|
| `sm` | `$typography.label2` (t7Bold) | 14px | Bold |
| `md` | `$typography.label1` (t5Bold) | 16px | Bold |
| `lg` | `$typography.label1` (t5Bold) | 16px | Bold |

---

## 4. Color Spec

### variant="primary"

| State | Container BG | Container Stroke | Label | Icon |
|-------|-------------|------------------|-------|------|
| **enabled** | `$color.bg.brand` | `transparent` | `$color.fg.on-brand` | `$color.fg.on-brand` |
| **hovered** | `$color.bg.brand-hover` | `transparent` | `$color.fg.on-brand` | `$color.fg.on-brand` |
| **pressed** | `$color.bg.brand-pressed` | `transparent` | `$color.fg.on-brand` | `$color.fg.on-brand` |
| **focused** | `$color.bg.brand` | `$color.stroke.brand` (ring) | `$color.fg.on-brand` | `$color.fg.on-brand` |
| **disabled** | `$color.bg.disabled` | `transparent` | `$color.fg.disabled` | `$color.fg.disabled` |
| **loading** | `$color.bg.brand` | `transparent` | (hidden) | spinner: `$color.fg.on-brand` |

### variant="secondary"

| State | Container BG | Container Stroke | Label | Icon |
|-------|-------------|------------------|-------|------|
| **enabled** | `transparent` | `$color.stroke.neutral-strong` | `$color.fg.neutral` | `$color.fg.neutral` |
| **hovered** | `$color.bg.neutral-hover` | `$color.stroke.neutral-strong` | `$color.fg.neutral` | `$color.fg.neutral` |
| **pressed** | `$color.bg.neutral-pressed` | `$color.stroke.neutral-strong` | `$color.fg.neutral` | `$color.fg.neutral` |
| **focused** | `transparent` | `$color.stroke.brand` (ring) | `$color.fg.neutral` | `$color.fg.neutral` |
| **disabled** | `transparent` | `$color.stroke.disabled` | `$color.fg.disabled` | `$color.fg.disabled` |
| **loading** | `transparent` | `$color.stroke.neutral-strong` | (hidden) | spinner: `$color.fg.neutral` |

### variant="tertiary"

| State | Container BG | Container Stroke | Label | Icon |
|-------|-------------|------------------|-------|------|
| **enabled** | `transparent` | `transparent` | `$color.fg.brand` | `$color.fg.brand` |
| **hovered** | `$color.bg.brand-weak` | `transparent` | `$color.fg.brand` | `$color.fg.brand` |
| **pressed** | `$color.bg.neutral-pressed` | `transparent` | `$color.fg.brand` | `$color.fg.brand` |
| **focused** | `transparent` | `$color.stroke.brand` (ring) | `$color.fg.brand` | `$color.fg.brand` |
| **disabled** | `transparent` | `transparent` | `$color.fg.disabled` | `$color.fg.disabled` |

### variant="destructive"

| State | Container BG | Container Stroke | Label | Icon |
|-------|-------------|------------------|-------|------|
| **enabled** | `$color.bg.critical` | `transparent` | `$color.fg.on-brand` | `$color.fg.on-brand` |
| **hovered** | `$color.palette.red-600` | `transparent` | `$color.fg.on-brand` | `$color.fg.on-brand` |
| **pressed** | `$color.palette.red-700` | `transparent` | `$color.fg.on-brand` | `$color.fg.on-brand` |
| **focused** | `$color.bg.critical` | `$color.stroke.critical` (ring) | `$color.fg.on-brand` | `$color.fg.on-brand` |
| **disabled** | `$color.bg.disabled` | `transparent` | `$color.fg.disabled` | `$color.fg.disabled` |

---

## 5. Radius Spec

모든 size에서 동일:

| Token | Value |
|-------|-------|
| `$radius.sm` | 8px |

---

## 6. Elevation Spec

| State | Elevation |
|-------|-----------|
| 모든 상태 | `$elevation.none` |

> Button은 평면 요소로, 그림자를 사용하지 않습니다.

---

## 7. Motion Spec

| Transition | Duration | Easing | 속성 |
|-----------|----------|--------|------|
| 색상 전환 | `$motion.duration.fast` (150ms) | `$motion.easing.standard` | `background-color`, `border-color`, `color` |
| 포커스 링 | `$motion.duration.fast` (150ms) | `$motion.easing.standard` | `box-shadow` |
| 로딩 전환 | `$motion.duration.normal` (250ms) | `$motion.easing.enter` | `opacity` (label↔spinner) |
| 스피너 회전 | `700ms` | `linear` | `transform: rotate` (무한 반복) |

---

## 8. Loading State 상세

```
Loading 전환:
1. Label opacity → 0 (250ms, enter easing)
2. Spinner opacity → 1 (250ms, enter easing)
3. 버튼 인터랙션 비활성 (pointer-events: none)
4. aria-busy="true"

Spinner 사양:
- 크기: sm=16px, md=20px, lg=20px
- 선 굵기: 2px
- 색상: Label과 동일 토큰
```

---

## 9. Width 모드

| Mode | 동작 |
|------|------|
| `hug` | 콘텐츠(아이콘 + 라벨 + 패딩)에 맞춤. `min-width` 적용 |
| `fill` | 부모 컨테이너 너비 100%. `min-width` 무시 |

모바일 하단 CTA는 일반적으로 `width="fill"` + `size="lg"`를 사용합니다.
