# BottomSheet — Style

## Anatomy Tokens

```
┌─────────────────────────────────────────┐
│            handle-bar                   │  $color.palette.gray-300
├─────────────────────────────────────────┤
│  header                                 │  height: 56px
├─────────────────────────────────────────┤
│                                         │
│  content                                │  padding: 16px
│                                         │
├─────────────────────────────────────────┤
│  footer                                 │  padding: 16px
└─────────────────────────────────────────┘
        ↑ container (bg, radius, elevation)
```

---

## Layout

| Element | Property | Value |
|---|---|---|
| **Container** | width | `100%` (mobile viewport) |
| | max-height | `90vh` |
| | overflow | `hidden` (content area scrolls independently) |
| **Handle bar** | width | `36px` |
| | height | `4px` |
| | alignment | Centered horizontally |
| | margin-top | `$dimension.x2` (8 px) |
| | margin-bottom | `$dimension.x2` (8 px) |
| | border-radius | `2px` (pill shape) |
| **Header** | height | `56px` |
| | padding-inline | `$dimension.x4` (16 px) |
| | alignment | Title start-aligned, close button end-aligned, both vertically centered |
| **Content area** | padding | `$dimension.x4` (16 px) |
| | overflow-y | `auto` |
| **Footer** | padding | `$dimension.x4` (16 px) |
| | border-top | `1px solid $color.border.neutral` |

---

## Color

| Element | Token | Resolved Value |
|---|---|---|
| Container background | `$color.bg.neutral` | White (#FFFFFF) / Dark mode neutral surface |
| Handle bar | `$color.palette.gray-300` | #D1D5DB |
| Scrim (modal variant) | `$color.bg.overlay` | rgba(0, 0, 0, 0.45) |
| Header title | `$color.fg.neutral` | #111827 |
| Close icon | `$color.fg.neutral-weak` | #6B7280 |
| Footer border | `$color.border.neutral` | #E5E7EB |

---

## Radius

| Edge | Token | Value |
|---|---|---|
| Top-left | `$radius.lg` | `16px` |
| Top-right | `$radius.lg` | `16px` |
| Bottom-left | — | `0` |
| Bottom-right | — | `0` |

When the sheet is expanded to full height (`snapPoint = 1.0`), the top radius may animate to `0` so the sheet appears flush with the status bar.

---

## Elevation

| Token | Usage |
|---|---|
| `$elevation.high` | Applied to the container. Produces a prominent shadow that separates the sheet from the underlying content. |

Shadow specification (reference):

```
box-shadow:
  0  -4px  16px  rgba(0, 0, 0, 0.08),
  0  -1px   4px  rgba(0, 0, 0, 0.04);
```

---

## Motion

### Enter (slide up + scrim fade)

| Property | Token / Value |
|---|---|
| Transform | `translateY(100%)` to `translateY(0)` |
| Duration | `$motion.duration.slow` (300 ms) |
| Easing | `$motion.easing.enter` — deceleration curve `cubic-bezier(0.0, 0.0, 0.2, 1.0)` |
| Scrim opacity | `0` to `1` over the same duration |

### Exit (slide down + scrim fade)

| Property | Token / Value |
|---|---|
| Transform | `translateY(0)` to `translateY(100%)` |
| Duration | `$motion.duration.slow` (300 ms) |
| Easing | `$motion.easing.exit` — acceleration curve `cubic-bezier(0.4, 0.0, 1.0, 1.0)` |
| Scrim opacity | `1` to `0` over the same duration |

### Snap Transition

| Property | Token / Value |
|---|---|
| Transform | Between snap point positions |
| Duration | `$motion.duration.normal` (200 ms) |
| Easing | `$motion.easing.standard` — `cubic-bezier(0.4, 0.0, 0.2, 1.0)` |

### Reduced Motion

When `prefers-reduced-motion: reduce` is active, all translate animations are disabled. The sheet appears and disappears with a simple opacity fade using `$motion.duration.normal`.
