# Motion

> 애니메이션 Duration, Easing, 전환 효과 토큰

---

## 개요

모션은 UI 요소의 상태 변화와 화면 전환에 **자연스러운 연속성**을 부여합니다. Carmore의 모션 시스템은 예약 플로우의 각 단계를 매끄럽게 연결하고, 사용자에게 시스템의 반응성을 전달합니다.

### 모션 원칙

1. **목적이 있는 움직임**: 모든 애니메이션은 상태 변화를 전달하거나 공간적 관계를 설명합니다
2. **빠르고 가벼운**: 사용자의 작업을 지연시키지 않습니다
3. **일관된 리듬**: 같은 유형의 전환에 같은 duration/easing을 사용합니다

---

## 1. Duration (지속 시간)

| Token | Value | 용도 |
|-------|-------|------|
| `$motion.duration.instant` | 0ms | 즉시 전환 (색상 변경 등) |
| `$motion.duration.fast` | 150ms | 호버/포커스 상태, 색상 전환, 아이콘 변경 |
| `$motion.duration.normal` | 250ms | 일반 전환, 드롭다운 열림/닫힘, 칩 토글 |
| `$motion.duration.slow` | 350ms | BottomSheet 슬라이드, Dialog 등장/퇴장 |
| `$motion.duration.slower` | 500ms | 페이지 전환, 대형 패널 애니메이션 |

---

## 2. Easing (가감속 곡선)

| Token | Value | 용도 |
|-------|-------|------|
| `$motion.easing.standard` | `cubic-bezier(0.4, 0.0, 0.2, 1.0)` | 일반적인 전환 (기본값) |
| `$motion.easing.enter` | `cubic-bezier(0.0, 0.0, 0.2, 1.0)` | 화면에 등장하는 요소 (decelerate) |
| `$motion.easing.exit` | `cubic-bezier(0.4, 0.0, 1.0, 1.0)` | 화면에서 퇴장하는 요소 (accelerate) |
| `$motion.easing.spring` | `cubic-bezier(0.175, 0.885, 0.32, 1.275)` | 탄성 효과 (토글, 바운스) |

---

## 3. 컴포넌트별 모션 매핑

| 컴포넌트 / 인터랙션 | Duration | Easing | 속성 |
|---------------------|----------|--------|------|
| Button 색상 전환 (hover/press) | `fast` (150ms) | `standard` | `background-color`, `border-color` |
| Button 로딩 스피너 등장 | `normal` (250ms) | `enter` | `opacity`, `transform` |
| TextField 포커스 테두리 | `fast` (150ms) | `standard` | `border-color`, `box-shadow` |
| TextField 에러 흔들기 | `fast` (150ms) | `spring` | `transform` (translateX) |
| Card 호버 그림자 | `normal` (250ms) | `standard` | `box-shadow`, `transform` |
| FilterChip 토글 | `fast` (150ms) | `standard` | `background-color`, `color` |
| BottomSheet 슬라이드 업 | `slow` (350ms) | `enter` | `transform` (translateY) |
| BottomSheet 슬라이드 다운 | `slow` (350ms) | `exit` | `transform` (translateY) |
| BottomSheet 스크림 | `slow` (350ms) | `standard` | `opacity` |
| Dialog 등장 | `slow` (350ms) | `enter` | `opacity`, `transform` (scale) |
| Dialog 퇴장 | `normal` (250ms) | `exit` | `opacity`, `transform` (scale) |
| 스켈레톤 펄스 | `slower` (500ms) | `standard` | `opacity` (무한 반복) |
| 페이지 전환 | `slower` (500ms) | `standard` | `opacity`, `transform` |

---

## 4. CSS 구현 예시

```css
:root {
  /* Duration */
  --motion-duration-instant: 0ms;
  --motion-duration-fast: 150ms;
  --motion-duration-normal: 250ms;
  --motion-duration-slow: 350ms;
  --motion-duration-slower: 500ms;

  /* Easing */
  --motion-easing-standard: cubic-bezier(0.4, 0.0, 0.2, 1.0);
  --motion-easing-enter: cubic-bezier(0.0, 0.0, 0.2, 1.0);
  --motion-easing-exit: cubic-bezier(0.4, 0.0, 1.0, 1.0);
  --motion-easing-spring: cubic-bezier(0.175, 0.885, 0.32, 1.275);
}

/* 사용 예시: Button */
.button {
  transition:
    background-color var(--motion-duration-fast) var(--motion-easing-standard),
    border-color var(--motion-duration-fast) var(--motion-easing-standard);
}

/* 사용 예시: BottomSheet */
.bottom-sheet {
  transition: transform var(--motion-duration-slow) var(--motion-easing-enter);
}
```

---

## 5. 접근성: 모션 감소 (Reduced Motion)

`prefers-reduced-motion: reduce` 미디어 쿼리를 존중하여 모션을 최소화합니다.

```css
@media (prefers-reduced-motion: reduce) {
  * {
    animation-duration: 0.01ms !important;
    transition-duration: 0.01ms !important;
  }
}
```

- 모든 애니메이션을 즉시 전환으로 대체합니다
- 스켈레톤 펄스 애니메이션을 정지합니다
- BottomSheet/Dialog는 즉시 나타나고 사라집니다

### iOS

```swift
UIAccessibility.isReduceMotionEnabled
```

### Android

```kotlin
Settings.Global.getFloat(contentResolver, Settings.Global.ANIMATOR_DURATION_SCALE)
```

---

## 6. 사용 가이드라인

### DO

- 상태 변화에는 항상 전환 효과를 적용합니다 (깜빡임 방지)
- 같은 유형의 인터랙션에 같은 duration/easing을 사용합니다
- `prefers-reduced-motion`을 반드시 지원합니다

### DON'T

- 300ms 이상의 delay를 인터랙션 피드백에 사용하지 않습니다
- 장식적 애니메이션으로 로딩 시간을 늘리지 않습니다
- 자동 재생 애니메이션을 5초 이상 반복하지 않습니다
- 깜빡임(3Hz 이상)이나 빠른 화면 전환을 사용하지 않습니다 (광과민성 발작 위험)
