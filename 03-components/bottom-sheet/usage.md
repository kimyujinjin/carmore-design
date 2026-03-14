# BottomSheet

## Description

BottomSheet is a surface that slides up from the bottom edge of the screen to present supplementary content without navigating away from the current view. It is the primary mobile pattern in Carmore for progressive disclosure of filters, date pickers, and option selectors.

Two variants exist:

| Variant | Scrim | Default Height | Dismissible |
|---|---|---|---|
| **modal** | Yes (overlay behind sheet) | Depends on content / snap points | Yes — drag down or tap scrim |
| **persistent** | No | Partial (collapsed snap point) | No — remains visible; user can expand or collapse |

### When Carmore Uses BottomSheet

- **Filter panels** — vehicle type, price range, fuel type, pickup location radius.
- **Date pickers** — rental period or accommodation check-in / check-out selection.
- **Vehicle & room option selectors** — insurance add-ons, child seat, extra driver, room upgrades.

---

## Anatomy

```
┌──────────────────────────────┐
│         ── handle ──         │  1. Handle bar
├──────────────────────────────┤
│  Title                    ✕  │  2. Header (title + close button)
├──────────────────────────────┤
│                              │
│     Scrollable content       │  3. Content area
│                              │
├──────────────────────────────┤
│  [ Primary CTA button ]      │  4. Footer with CTA
└──────────────────────────────┘
```

1. **Handle bar** — A small horizontal bar at the top that signals the sheet is draggable.
2. **Header** — Contains a title string and an optional close (✕) icon button aligned to the trailing edge.
3. **Content area** — Scrollable region that holds the body of the sheet (lists, forms, pickers, etc.).
4. **Footer** — A sticky bottom area containing the primary call-to-action button (e.g., "필터 적용", "날짜 선택 완료").

---

## Options

| Property | Type | Default | Description |
|---|---|---|---|
| `variant` | `"modal"` \| `"persistent"` | `"modal"` | Controls whether a scrim is shown and whether the sheet blocks interaction with the content behind it. |
| `title` | `string` | — | Text displayed in the header. |
| `showHandle` | `boolean` | `true` | Whether to render the drag handle bar. |
| `snapPoints` | `number[]` | `[0.5, 1.0]` | Array of height ratios (0–1) the sheet snaps to. `1.0` means full screen. |
| `dismissible` | `boolean` | `true` | Whether the user can dismiss the sheet by dragging down or tapping the scrim. Set to `false` for persistent sheets or flows that require explicit action. |

---

## Interactions

| Gesture / Input | Behavior |
|---|---|
| **Drag handle or header down** | Collapses to the next lower snap point; if already at the lowest, dismisses the sheet (when `dismissible` is `true`). |
| **Drag handle or header up** | Expands to the next higher snap point. |
| **Tap scrim** | Dismisses the sheet (`modal` variant, `dismissible: true` only). |
| **Swipe down on content** | If content is scrolled to top, the swipe transfers to the sheet and begins collapsing it. |
| **ESC key (web)** | Dismisses the sheet when `dismissible` is `true`. |
| **Android back button** | Dismisses the sheet when `dismissible` is `true`. |

---

## Do / Don't

### Do

- Use BottomSheet for secondary or supplementary content on mobile (filters, selectors, additional options).
- Provide at least two snap points so users can preview content before fully expanding.
- Always include a clear CTA in the footer when the sheet involves a selection or decision.

### Don't

- Don't place critical first-time content (e.g., onboarding, essential alerts) inside a BottomSheet — use a Dialog or a full-screen view instead.
- Don't nest a BottomSheet inside another BottomSheet.
- Don't use BottomSheet on desktop viewports; convert it to a **side panel** or inline expanded section at the `$breakpoint.md` (768 px) threshold and above.

---

## Platform Differences

| Platform | Implementation Notes |
|---|---|
| **iOS** | Wraps `UISheetPresentationController` with custom detents mapped to `snapPoints`. Handle bar uses the native appearance. |
| **Android** | Wraps `BottomSheetBehavior` from Material Components. Peek height maps to the first snap point. |
| **Web** | Custom implementation using CSS transforms and pointer / touch event listeners. Uses `position: fixed` at the bottom of the viewport. |

On all platforms the visual design, spacing, and animation curves remain consistent with Carmore design tokens.

---

## Accessibility

| Attribute | Value / Behavior |
|---|---|
| `role` | `dialog` |
| `aria-modal` | `true` (modal variant) |
| **Focus trap** | When the modal variant opens, focus is trapped inside the sheet. On dismiss, focus returns to the trigger element. |
| **ESC to dismiss** | Pressing `Escape` closes the sheet (web). |
| **Screen reader announcement** | The title is announced when the sheet opens. Content changes within the sheet should use live regions where appropriate. |
| **Reduced motion** | When the user prefers reduced motion, the slide animation is replaced with a simple opacity fade. |
