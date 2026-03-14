# Dialog — Style

## Anatomy Tokens

```
┌─ scrim ($color.bg.overlay) ──────────────┐
│                                          │
│   ┌──── container ───────────────┐       │
│   │  padding: $dimension.x6      │       │
│   │                              │       │
│   │  [title]         ← title3    │       │
│   │      ↕ 8px                   │       │
│   │  [description]   ← body1    │       │
│   │      ↕ 24px                  │       │
│   │  [secondary] [primary]       │       │
│   │      ↔ 8px button gap        │       │
│   └──────────────────────────────┘       │
│                                          │
└──────────────────────────────────────────┘
```

---

## Layout

| Element | Property | Value |
|---|---|---|
| **Container** | min-width | `280px` |
| | max-width | `400px` |
| | padding | `$dimension.x6` (24 px) |
| | alignment | Centered horizontally and vertically in the viewport |
| **Title → Description** | gap | `$dimension.x2` (8 px) |
| **Description → Buttons** | gap | `$dimension.x6` (24 px) |
| **Button area** | layout | Horizontal, trailing-aligned |
| | gap between buttons | `$dimension.x2` (8 px) |
| **Buttons** | min-width | `64px` |
| | padding-inline | `$dimension.x4` (16 px) |
| | height | `44px` |

On viewports narrower than `320px`, buttons stack vertically (primary on top) with the same 8 px gap.

---

## Typography

| Element | Token | Resolved Spec |
|---|---|---|
| Title | `$typography.title3` | Font: Pretendard SemiBold, 18 px / 26 px line-height |
| Description | `$typography.body1` | Font: Pretendard Regular, 16 px / 24 px line-height |
| Button labels | `$typography.label1` | Font: Pretendard Medium, 15 px / 20 px line-height |

---

## Color

### Default (confirm / alert)

| Element | Token | Resolved Value |
|---|---|---|
| Container background | `$color.bg.neutral` | #FFFFFF (light) |
| Scrim | `$color.bg.overlay` | rgba(0, 0, 0, 0.45) |
| Title | `$color.fg.neutral` | #111827 |
| Description | `$color.fg.neutral-weak` | #6B7280 |
| Primary button background | `$color.bg.brand` | Carmore Blue (#1A6DFF) |
| Primary button label | `$color.fg.on-brand` | #FFFFFF |
| Secondary button background | `$color.bg.neutral-subtle` | #F3F4F6 |
| Secondary button label | `$color.fg.neutral` | #111827 |

### Destructive Variant

| Element | Token | Resolved Value |
|---|---|---|
| Primary button background | `$color.bg.critical` | #DC2626 |
| Primary button label | `$color.fg.on-critical` | #FFFFFF |

All other elements remain the same as the default.

---

## Radius

| Element | Token | Value |
|---|---|---|
| Container | `$radius.xl` | `20px` |
| Buttons | `$radius.md` | `10px` |

---

## Elevation

| Token | Usage |
|---|---|
| `$elevation.high` | Applied to the container to lift it above the scrim. |

Shadow specification (reference):

```
box-shadow:
  0  8px  24px  rgba(0, 0, 0, 0.12),
  0  2px   8px  rgba(0, 0, 0, 0.06);
```

---

## Motion

### Enter

| Property | From | To | Duration | Easing |
|---|---|---|---|---|
| `transform: scale` | `0.95` | `1.0` | `$motion.duration.slow` (300 ms) | `$motion.easing.enter` — `cubic-bezier(0.0, 0.0, 0.2, 1.0)` |
| `opacity` | `0` | `1` | `$motion.duration.slow` (300 ms) | `$motion.easing.enter` |
| Scrim opacity | `0` | `1` | `$motion.duration.slow` (300 ms) | `$motion.easing.standard` |

### Exit

| Property | From | To | Duration | Easing |
|---|---|---|---|---|
| `opacity` | `1` | `0` | `$motion.duration.normal` (200 ms) | `$motion.easing.exit` — `cubic-bezier(0.4, 0.0, 1.0, 1.0)` |
| Scrim opacity | `1` | `0` | `$motion.duration.normal` (200 ms) | `$motion.easing.exit` |

The exit animation does not include a scale transform to keep the dismiss feeling snappy and non-distracting.

### Reduced Motion

When `prefers-reduced-motion: reduce` is active, scale and translate animations are disabled. The dialog appears and disappears with a simple opacity crossfade at `$motion.duration.normal`.
