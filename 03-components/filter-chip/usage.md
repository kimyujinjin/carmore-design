# FilterChip

> 검색 결과를 필터링하는 컴팩트한 토글 요소

---

## 1. 설명 (Description)

FilterChip은 사용자가 탭하여 **필터 조건을 설정하거나 해제**하는 컴포넌트입니다. Carmore에서는 렌터카 검색 시 차량 유형(세단/SUV/밴), 가격대, 연료 타입 필터, 숙소 검색 시 편의시설(Wi-Fi/Pool/Parking), 성급 필터 등에 사용됩니다.

FilterChip의 variant는 **필터 동작 방식**에 따라 선택합니다:
- **Toggle**: 단순 on/off 토글로 필터를 활성화/비활성화
- **Selection**: 탭하면 드롭다운/바텀시트를 열어 세부 옵션 선택
- **Removable**: 이미 선택된 필터를 X 버튼으로 제거

---

## 2. 해부도 (Anatomy)

```
┌───────────────────────────────────────────┐
│  ①[Icon]  ②[Label]  ③[Count]  ④[Trail]   │  ⑤ Container (pill)
└───────────────────────────────────────────┘
```

| # | Part | 필수 여부 | 설명 |
|---|------|-----------|------|
| ① | Leading Icon | 선택 | 필터 카테고리를 나타내는 아이콘 (예: 연료 아이콘) |
| ② | Label | 필수 | 필터 이름 텍스트 (예: "세단", "Wi-Fi") |
| ③ | Count Badge | 선택 | 선택된 하위 옵션 수 (예: "3") |
| ④ | Trailing Icon | 선택 | variant에 따라 chevron(↓) 또는 close(✕) 아이콘 |
| ⑤ | Container | 필수 | pill 형태의 외곽 컨테이너 |

---

## 3. 옵션 (Options / Props)

| Property | Type | Values | Default | 설명 |
|----------|------|--------|---------|------|
| `variant` | enum | `"toggle"` \| `"selection"` \| `"removable"` | `"toggle"` | 칩의 동작 방식 |
| `selected` | boolean | `true` \| `false` | `false` | 선택(활성) 상태 |
| `disabled` | boolean | `true` \| `false` | `false` | 비활성 상태 |
| `label` | string | — | 필수 | 필터 라벨 텍스트 |
| `leadingIcon` | icon | — | `undefined` | 라벨 앞 아이콘 |
| `count` | number | — | `undefined` | 선택된 옵션 수 배지 |

---

## 4. 인터랙션 (Interactions)

| 입력 | 동작 |
|------|------|
| **Tap** (toggle) | selected 상태 토글 (on ↔ off) |
| **Tap** (selection) | 드롭다운 또는 바텀시트 열기 |
| **Tap ✕** (removable) | 해당 필터 제거 |
| **Hover** (Web) | hover 스타일 전환 |
| **Keyboard Focus** | 포커스 링 표시 |
| **Enter / Space** (키보드) | Tap과 동일한 액션 실행 |
| **Horizontal Scroll** | 칩 그룹에서 좌우 스크롤로 추가 칩 확인 |
| **Disabled** | 시각적으로 흐려짐, 모든 인터랙션 무시 |

---

## 5. 가이드라인 (Do & Don't)

### DO

- ✅ **칩 그룹은 수평 스크롤로 구성합니다** — 화면 밖 칩은 스크롤로 접근
  ```
  ← [세단] [SUV] [밴] [전기차] [하이브리드] →  (수평 스크롤)
  ```

- ✅ **라벨은 3단어 이하로 간결하게 유지합니다**
  ```
  "Wi-Fi", "수영장", "무료 주차"
  ```

- ✅ **초기 상태에서 칩은 1줄만 노출합니다** — 추가 필터는 "더보기" 또는 스크롤

- ✅ **선택된 칩은 시각적으로 명확히 구분합니다** (브랜드 색상 활용)

- ✅ **selection variant는 chevron(↓)으로 추가 옵션이 있음을 표시합니다**
  ```
  [가격대 ↓]  →  탭 시 가격 범위 바텀시트 열림
  ```

### DON'T

- ❌ **같은 줄에서 서로 다른 variant의 칩을 혼용하지 않습니다**
  ```
  ❌ [세단] [가격대 ↓] [Wi-Fi ✕]    ← toggle, selection, removable 혼합
  ✅ [세단] [SUV] [밴]              ← 모두 toggle
  ```

- ❌ **칩을 줄바꿈(wrap)하여 여러 줄로 배치하지 않습니다** — 수평 스크롤 사용
  ```
  ❌ [세단] [SUV] [밴]
     [전기차] [하이브리드]            ← 2줄 wrap
  ✅ ← [세단] [SUV] [밴] [전기차] → ← 1줄 스크롤
  ```

- ❌ **라벨이 4단어 이상이 되지 않도록 합니다** — 긴 텍스트는 줄임 처리

- ❌ **칩을 주요 액션 트리거로 사용하지 않습니다** (필터 용도로만 사용)

---

## 6. 플랫폼 차이 (Platform Differences)

| 항목 | Web | iOS | Android |
|------|-----|-----|---------|
| Hover 상태 | 지원 | 미지원 (터치) | 미지원 (터치) |
| 포커스 링 | 키보드 포커스 시 표시 | VoiceOver 포커스 | TalkBack 포커스 |
| 스크롤 표시 | 스크롤바 숨김, 화살표 힌트 | 관성 스크롤 | 관성 스크롤 |
| 햅틱 피드백 | 없음 | 탭 시 경미한 햅틱 | 탭 시 경미한 햅틱 |
| 높이 | 36px | 36pt | 36dp |
| 최소 터치 타겟 | 36px (chip 자체) | 44pt (여백 포함) | 48dp (여백 포함) |

---

## 7. 접근성 (Accessibility)

| 속성 | 값 |
|------|-----|
| **Role** (toggle) | `checkbox` |
| **Role** (selection) | `button` |
| **Role** (removable) | `button` |
| **aria-pressed** | toggle variant에서 selected 상태 시 `true`, 미선택 시 `false` |
| **aria-expanded** | selection variant에서 드롭다운 열림 시 `true` |
| **aria-label** | 라벨 텍스트와 동일 (count 포함 시 "가격대, 3개 선택됨") |
| **aria-disabled** | disabled 상태에서 `true` |
| **키보드** | `Tab`으로 포커스 이동, `Enter`/`Space`로 토글/열기/제거 |
| **스크린 리더** | toggle: "[라벨], 체크박스, 선택됨/선택 안 됨" / selection: "[라벨], 버튼" / removable: "[라벨] 필터 제거, 버튼" |
| **칩 그룹** | `role="group"` + `aria-label="필터"` |

---

## 8. Carmore 사용 예시

### 렌터카 검색 필터

```
┌─────────────────────────────────────────────────┐
│  ← [세단] [SUV] [밴] [전기차] [하이브리드] →      │  ← toggle chips, 수평 스크롤
│                                                 │
│  ← [가격대 ↓] [보험 포함 ↓] [연료 ↓] →            │  ← selection chips
└─────────────────────────────────────────────────┘
```

### 숙소 검색 — 선택된 필터 표시

```
┌─────────────────────────────────────────────────┐
│  적용된 필터:                                     │
│  [Wi-Fi ✕] [수영장 ✕] [무료 주차 ✕]               │  ← removable chips
└─────────────────────────────────────────────────┘
```
