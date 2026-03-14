# Dialog

## Description

Dialog is a modal overlay that interrupts the user to request a decision or acknowledgment. It appears centered on the screen with a scrim behind it and requires the user to take action before continuing.

Carmore uses Dialog for high-stakes moments: confirming a booking, cancelling a reservation, acknowledging a session timeout, or verifying a destructive action.

### Variants

| Variant | Actions | Use Case |
|---|---|---|
| **alert** | Single action ("확인") | Informational notice that requires acknowledgment — e.g., session timeout, booking confirmed. |
| **confirm** | Two actions ("취소" / "확인") | Decision point — e.g., "예약을 확정할까요?" |
| **destructive** | Two actions ("취소" / "삭제") — primary action styled in red | Irreversible action — e.g., "예약을 취소하시겠습니까?" |

### When Carmore Uses Dialog

- **Booking confirmation** — "예약을 확정할까요?" (confirm variant)
- **Cancellation** — "예약을 취소하시겠습니까? 취소 수수료가 발생할 수 있습니다." (destructive variant)
- **Session timeout** — "세션이 만료되었습니다. 다시 로그인해 주세요." (alert variant)
- **Account deletion** — "계정을 삭제하시겠습니까? 이 작업은 되돌릴 수 없습니다." (destructive variant)

---

## Anatomy

```
┌─ scrim (full viewport) ──────────────────┐
│                                          │
│   ┌──────────────────────────────┐       │
│   │  Title                       │  1    │
│   │  Description text goes here  │  2    │
│   │                              │       │
│   │         [ 취소 ]  [ 확인 ]    │  3    │
│   └──────────────────────────────┘       │
│                                          │
└──────────────────────────────────────────┘
```

1. **Title** — A short, direct heading that states the purpose of the dialog.
2. **Description** — One or two sentences providing context or consequences.
3. **Action area** — Contains one or two buttons. The primary action is always on the trailing (right) side.

---

## Options

| Property | Type | Default | Description |
|---|---|---|---|
| `variant` | `"alert"` \| `"confirm"` \| `"destructive"` | `"confirm"` | Determines the number and styling of action buttons. |
| `title` | `string` | — | Heading text displayed at the top of the dialog. Required. |
| `description` | `string` | — | Body text providing additional context. Optional but strongly recommended. |
| `primaryLabel` | `string` | `"확인"` | Label for the primary (trailing) action button. |
| `secondaryLabel` | `string` | `"취소"` | Label for the secondary (leading) action button. Not shown for `alert` variant. |
| `dismissible` | `boolean` | `true` for `confirm`, `false` for `alert` and `destructive` | Whether the dialog can be closed by tapping the scrim or pressing ESC. Destructive dialogs require an explicit button tap. |

---

## Interactions

| Input | Behavior |
|---|---|
| **Tap primary button** | Executes the primary action and closes the dialog. |
| **Tap secondary button** | Cancels and closes the dialog (confirm / destructive variants). |
| **Tap scrim** | Closes the dialog only when `dismissible` is `true`. Equivalent to tapping the secondary button. |
| **ESC key (web) / Back (Android)** | Closes the dialog only when `dismissible` is `true`. |

---

## Do / Don't

### Do

- Keep the title concise and action-oriented (e.g., "예약을 취소할까요?").
- Keep the description under two sentences. Provide just enough context for the user to make a decision.
- Use the **destructive** variant whenever an action cannot be undone; ensure the primary button label explicitly describes the action (e.g., "삭제", "취소하기") rather than a generic "확인".

### Don't

- Don't use Dialog for complex forms or multi-step flows. Use a full-screen view or BottomSheet instead.
- Don't stack multiple Dialogs. If a second confirmation is needed, redesign the flow.
- Don't use vague button labels. "네" / "아니요" is less clear than "삭제" / "유지하기".
- Don't make the destructive primary button the default focus color — it must be red to signal danger.

---

## Platform Differences

| Platform | Implementation Notes |
|---|---|
| **iOS** | Wraps `UIAlertController` for alert variant. Confirm and destructive variants use a custom presented view controller for design-token consistency. |
| **Android** | Uses `MaterialAlertDialogBuilder` with Carmore theme overlay for colors, typography, and shape. |
| **Web** | Rendered as a custom component using `<dialog>` element (or polyfill). Positioned with `position: fixed` and flexbox centering. |

Visual appearance is identical across platforms, governed by shared design tokens.

---

## Accessibility

| Attribute | Value / Behavior |
|---|---|
| `role` | `alertdialog` |
| `aria-modal` | `true` |
| `aria-labelledby` | Points to the title element. |
| `aria-describedby` | Points to the description element. |
| **Focus trap** | Focus is trapped within the dialog while it is open. On dismiss, focus returns to the element that triggered the dialog. |
| **Auto-focus** | The primary action button receives focus when the dialog opens. For destructive dialogs, the secondary ("취소") button receives focus instead to prevent accidental confirmation. |
| **ESC to dismiss** | Closes the dialog when `dismissible` is `true`. |
| **Screen reader** | The title and description are announced immediately when the dialog opens. |
