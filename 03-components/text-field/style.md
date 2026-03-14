# TextField — Style Spec

> 토큰 매핑, 상태별 스펙, 레이아웃 치수

---

## 1. Anatomy 토큰 슬롯

| Part | Token Slot |
|------|-----------|
| Container | `background`, `border` (1px), `border-radius` |
| Label | `color`, `typography` |
| Input | `color`, `typography` |
| Placeholder | `color` |
| Prefix / Suffix Icon | `color`, `size` |
| Helper Text | `color`, `typography` |
| Error Text | `color`, `typography` |
| Character Counter | `color`, `typography` |
| Focus Ring | `color` (`$color.stroke.brand`), `offset` (2px), `width` (2px) |

---

## 2. Layout Spec

| Size | Height | Padding X | Padding Y | Icon Size | Icon-Input Gap |
|------|--------|-----------|-----------|-----------|---------------|
| `sm` | 36px | `$dimension.x3` (12px) | auto | `$icon.xs` (16px) | `$dimension.x2` (8px) |
| `md` | 44px | `$dimension.x3` (12px) | auto | `$icon.sm` (20px) | `$dimension.x2` (8px) |
| `lg` | 52px | `$dimension.x4` (16px) | auto | `$icon.sm` (20px) | `$dimension.x3` (12px) |

> Label은 Container 위 `$dimension.x1` (4px) 간격으로 배치됩니다.
> Helper / Error Text는 Container 아래 `$dimension.x1` (4px) 간격으로 배치됩니다.
> Character Counter는 Helper Text와 같은 줄 우측 정렬입니다.

---

## 3. Typography Spec

| Part | Size sm | Size md | Size lg |
|------|---------|---------|---------|
| Input | `$typography.body2` (t7Regular) — 14px Regular | `$typography.body1` (t5Regular) — 16px Regular | `$typography.body1` (t5Regular) — 16px Regular |
| Placeholder | Input과 동일 토큰 | Input과 동일 토큰 | Input과 동일 토큰 |
| Label | `$typography.caption1` (t8Medium) — 12px Medium | `$typography.caption1` (t8Medium) — 12px Medium | `$typography.caption1` (t8Medium) — 12px Medium |
| Helper / Error | `$typography.caption2` (t8Regular) — 12px Regular | `$typography.caption2` (t8Regular) — 12px Regular | `$typography.caption2` (t8Regular) — 12px Regular |
| Character Counter | `$typography.caption2` (t8Regular) — 12px Regular | `$typography.caption2` (t8Regular) — 12px Regular | `$typography.caption2` (t8Regular) — 12px Regular |

---

## 4. Color Spec

### variant="default"

| State | Container BG | Container Stroke | Label | Input | Placeholder | Icon | Helper Text |
|-------|-------------|------------------|-------|-------|-------------|------|-------------|
| **empty** | `$color.bg.neutral` | `$color.stroke.neutral` | `$color.fg.neutral` | — | `$color.fg.neutral-weakest` | `$color.fg.neutral-weak` | `$color.fg.neutral-weak` |
| **filled** | `$color.bg.neutral` | `$color.stroke.neutral` | `$color.fg.neutral` | `$color.fg.neutral` | — | `$color.fg.neutral-weak` | `$color.fg.neutral-weak` |
| **hovered** | `$color.bg.neutral` | `$color.stroke.neutral-strong` | `$color.fg.neutral` | `$color.fg.neutral` | `$color.fg.neutral-weakest` | `$color.fg.neutral-weak` | `$color.fg.neutral-weak` |
| **focused** | `$color.bg.neutral` | `$color.stroke.brand` | `$color.fg.brand` | `$color.fg.neutral` | `$color.fg.neutral-weakest` | `$color.fg.neutral` | `$color.fg.neutral-weak` |
| **error** | `$color.bg.neutral` | `$color.stroke.critical` | `$color.fg.critical` | `$color.fg.neutral` | `$color.fg.neutral-weakest` | `$color.fg.critical` | `$color.fg.critical` |
| **disabled** | `$color.bg.disabled` | `$color.stroke.disabled` | `$color.fg.disabled` | `$color.fg.disabled` | `$color.fg.disabled` | `$color.fg.disabled` | `$color.fg.disabled` |
| **readOnly** | `$color.bg.neutral-weak` | `transparent` | `$color.fg.neutral` | `$color.fg.neutral` | — | `$color.fg.neutral-weak` | `$color.fg.neutral-weak` |

### variant="search"

| State | Container BG | Container Stroke | Input | Placeholder | Search Icon | Clear Button |
|-------|-------------|------------------|-------|-------------|-------------|-------------|
| **empty** | `$color.bg.neutral` | `$color.stroke.neutral` | — | `$color.fg.neutral-weakest` | `$color.fg.neutral-weak` | (hidden) |
| **filled** | `$color.bg.neutral` | `$color.stroke.neutral` | `$color.fg.neutral` | — | `$color.fg.neutral-weak` | `$color.fg.neutral-weak` |
| **hovered** | `$color.bg.neutral` | `$color.stroke.neutral-strong` | `$color.fg.neutral` | `$color.fg.neutral-weakest` | `$color.fg.neutral-weak` | `$color.fg.neutral-weak` |
| **focused** | `$color.bg.neutral` | `$color.stroke.brand` | `$color.fg.neutral` | `$color.fg.neutral-weakest` | `$color.fg.neutral` | `$color.fg.neutral` |
| **disabled** | `$color.bg.disabled` | `$color.stroke.disabled` | `$color.fg.disabled` | `$color.fg.disabled` | `$color.fg.disabled` | (hidden) |

> Search variant는 Label, Helper Text, Error 상태를 사용하지 않습니다.

---

## 5. Radius Spec

모든 size에서 동일:

| Token | Value |
|-------|-------|
| `$radius.sm` | 8px |

---

## 6. Motion Spec

| Transition | Duration | Easing | 속성 |
|-----------|----------|--------|------|
| 포커스 전환 | `$motion.duration.fast` (150ms) | `$motion.easing.standard` | `border-color`, `box-shadow` |
| Label 색상 전환 | `$motion.duration.fast` (150ms) | `$motion.easing.standard` | `color` |
| 에러 Shake | `$motion.duration.fast` (150ms) | `$motion.easing.spring` | `transform: translateX` |
| Clear 버튼 표시 | `$motion.duration.fast` (150ms) | `$motion.easing.enter` | `opacity`, `scale` |

### 에러 Shake 상세

```
에러 Shake 애니메이션:
1. 에러 상태 진입 시 Container가 수평으로 흔들림
2. keyframes: 0ms → 0px, 30ms → -4px, 60ms → 4px, 90ms → -2px, 120ms → 2px, 150ms → 0px
3. easing: spring (빠른 감쇠)
4. 1회만 실행 후 정지
```

---

## 7. Search Variant 상세

```
Search variant 구조:
┌─────────────────────────────────────────┐
│  [🔍 Search Icon]  [Input]  [✕ Clear]  │
└─────────────────────────────────────────┘

Search Icon:
- 위치: prefix (좌측 고정)
- 크기: $icon.sm (20px) — 모든 size 동일
- 색상: 상태별 Color Spec 참조

Clear Button:
- 위치: suffix (우측)
- 크기: $icon.sm (20px)
- 표시 조건: input value가 비어있지 않을 때
- 터치 타겟: 최소 44×44px (접근성)
- 동작: 클릭 시 input value 초기화 + 포커스 유지
- 진입 애니메이션: opacity 0→1 + scale 0.8→1 (150ms, enter easing)
- 퇴장 애니메이션: opacity 1→0 (150ms, standard easing)
```

---

## 8. Focus Ring 상세

```
Focus Ring 사양 (키보드 포커스 시):
- offset: 2px (Container 외부)
- width: 2px
- color: $color.stroke.brand
- border-radius: Container radius + offset (10px)
- transition: $motion.duration.fast (150ms)

마우스 / 터치 포커스:
- Focus Ring 없음
- Container stroke 색상만 $color.stroke.brand로 전환
```

---

## 9. Character Counter 상세

| 상태 | 색상 |
|------|------|
| 기본 (여유 있음) | `$color.fg.neutral-weak` |
| 임계값 초과 (90% 이상) | `$color.fg.warning` |
| 최대 도달 (100%) | `$color.fg.critical` |

> Counter 형식: `{현재}/{최대}` (예: `128/500`)
> Counter는 Helper Text 우측에 같은 줄로 배치됩니다.
