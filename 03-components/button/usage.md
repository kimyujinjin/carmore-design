# Button

> 사용자의 주요 액션을 트리거하는 인터랙티브 요소

---

## 1. 설명

Button은 사용자가 탭/클릭하여 **작업을 실행**하는 컴포넌트입니다. Carmore에서는 "지금 예약", "검색", "필터 적용", "취소" 등 핵심 액션에 사용됩니다.

Button의 variant는 **액션의 중요도**에 따라 선택합니다:
- **Primary**: 화면의 가장 중요한 단일 액션
- **Secondary**: Primary를 보조하는 대안 액션
- **Tertiary**: 낮은 강조도의 부가 액션
- **Destructive**: 취소, 삭제 등 돌이키기 어려운 액션

---

## 2. 해부도 (Anatomy)

```
┌──────────────────────────────────────────┐
│  ①[Icon]  ②[Label]  ③[Icon]             │  ④ Container
└──────────────────────────────────────────┘
```

| # | Part | 필수 여부 | 설명 |
|---|------|-----------|------|
| ① | Leading Icon | 선택 | 라벨 앞 아이콘 |
| ② | Label | 필수 | 액션을 설명하는 텍스트 |
| ③ | Trailing Icon | 선택 | 라벨 뒤 아이콘 (화살표 등) |
| ④ | Container | 필수 | 배경, 테두리를 포함하는 외곽 |

---

## 3. 옵션 (Options)

| Property | Type | Values | Default | 설명 |
|----------|------|--------|---------|------|
| `variant` | enum | `"primary"` \| `"secondary"` \| `"tertiary"` \| `"destructive"` | `"primary"` | 시각적 변형 |
| `size` | enum | `"sm"` \| `"md"` \| `"lg"` | `"md"` | 크기 |
| `width` | enum | `"hug"` \| `"fill"` | `"hug"` | 콘텐츠 맞춤 또는 부모 너비 채움 |
| `disabled` | boolean | `true` \| `false` | `false` | 비활성 상태 |
| `loading` | boolean | `true` \| `false` | `false` | 로딩 중 (스피너 표시) |
| `leadingIcon` | icon | — | `undefined` | 라벨 앞 아이콘 |
| `trailingIcon` | icon | — | `undefined` | 라벨 뒤 아이콘 |

---

## 4. 인터랙션 (Interactions)

| 입력 | 동작 |
|------|------|
| **Click / Tap** | 액션 실행 |
| **Hover** (Web) | hover 스타일 전환 |
| **Keyboard Focus** | 포커스 링 표시 |
| **Enter / Space** (키보드) | 액션 실행 |
| **Loading 상태** | 라벨 → 스피너로 교체, 인터랙션 비활성 |
| **Disabled** | 시각적으로 흐려짐, 모든 인터랙션 무시 |

---

## 5. 가이드라인 (Do & Don't)

### DO

- ✅ **화면 영역 당 Primary 버튼은 1개만 사용합니다**
  ```
  [지금 예약] (primary)     [나중에 결정] (secondary)
  ```

- ✅ **라벨은 동사로 시작합니다** — 사용자가 어떤 일이 일어나는지 예측 가능
  ```
  "검색하기", "예약 확정", "필터 적용", "취소하기"
  ```

- ✅ **Destructive variant는 확인 단계를 거칩니다** (Dialog와 함께 사용)
  ```
  [예약 취소] → Dialog("정말 취소하시겠습니까?") → [취소 확정]
  ```

- ✅ **모바일 하단 CTA는 `width="fill"` + `size="lg"`를 사용합니다**

- ✅ **로딩 중에는 라벨 대신 스피너를 표시하고, 중복 클릭을 방지합니다**

### DON'T

- ❌ **같은 variant 버튼을 3개 이상 나란히 배치하지 않습니다**
  ```
  ❌ [Primary] [Primary] [Primary]
  ✅ [Primary] [Secondary] [Tertiary]
  ```

- ❌ **라벨 없이 아이콘만 사용하지 않습니다** (IconButton은 별도 컴포넌트)

- ❌ **라벨이 2줄 이상이 되지 않도록 합니다** — 간결하게 유지

- ❌ **Destructive 버튼을 기본 흐름의 Primary 액션으로 사용하지 않습니다**
  ```
  ❌ 예약 상세 페이지의 메인 CTA로 [예약 취소] 배치
  ```

---

## 6. 플랫폼 차이 (Platform Differences)

| 항목 | Web | iOS | Android |
|------|-----|-----|---------|
| Hover 상태 | 지원 | 미지원 (터치) | 미지원 (터치) |
| 포커스 링 | 키보드 포커스 시 표시 | VoiceOver 포커스 | TalkBack 포커스 |
| 햅틱 피드백 | 없음 | 탭 시 경미한 햅틱 | 탭 시 경미한 햅틱 |
| 하단 CTA 위치 | 페이지 내 또는 sticky footer | Safe area 위 | Navigation bar 위 |
| `size="lg"` 높이 | 52px | 52pt | 52dp |
| 최소 터치 타겟 | 44px | 44pt | 48dp |

---

## 7. 접근성 (Accessibility)

| 속성 | 값 |
|------|-----|
| **Role** | `button` |
| **aria-label** | 라벨 텍스트와 동일 (아이콘만 있을 경우 필수 지정) |
| **aria-disabled** | disabled 상태에서 `true` |
| **aria-busy** | loading 상태에서 `true` |
| **키보드** | `Tab`으로 포커스, `Enter`/`Space`로 실행 |
| **스크린 리더** | "[라벨], 버튼" 또는 "로딩 중, 버튼" (loading 시) |
| **색상 외 표시** | disabled는 색상 + opacity 변경으로 이중 표시 |

---

## 8. Carmore 사용 예시

### 검색 페이지

```
┌─────────────────────────────────────┐
│  어디로 가시나요?                     │  ← TextField
│  [날짜 선택]  [인원 선택]             │  ← Secondary buttons (sm)
│                                     │
│  ┌─────────────────────────────┐   │
│  │     🔍  렌터카 검색하기      │   │  ← Primary, lg, fill
│  └─────────────────────────────┘   │
└─────────────────────────────────────┘
```

### 예약 상세 하단

```
┌─────────────────────────────────────┐
│  [예약 변경]        [예약 취소]       │
│  secondary, md      destructive, md  │
└─────────────────────────────────────┘
```
