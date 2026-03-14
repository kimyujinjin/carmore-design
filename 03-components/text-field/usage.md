# TextField

> 사용자가 텍스트를 입력하는 폼 인터랙티브 요소

---

## 1. 설명

TextField는 사용자가 **텍스트를 직접 입력**하는 컴포넌트입니다. Carmore에서는 이름, 이메일, 전화번호, 날짜, 위치 검색, 후기 작성 등 핵심 입력 시나리오에 사용됩니다.

TextField의 variant는 **사용 맥락**에 따라 선택합니다:
- **Default**: 일반 폼 입력 (이름, 이메일, 전화번호, 날짜 등)
- **Search**: 검색 전용 (prefix 검색 아이콘 + 입력값이 있을 때 clear 버튼 자동 표시)

---

## 2. 해부도 (Anatomy)

```
         ①[Label]
┌──────────────────────────────────────────┐
│  ②[Prefix Icon]  ③[Input]  ④[Suffix]    │  ⑤ Container
└──────────────────────────────────────────┘
         ⑥[Helper / Error]     ⑦[Counter]
```

| # | Part | 필수 여부 | 설명 |
|---|------|-----------|------|
| ① | Label | 선택 | 입력 필드 위에 표시되는 라벨 텍스트 |
| ② | Prefix Icon | 선택 | 입력 영역 앞 아이콘 (Search variant에서는 검색 아이콘 고정) |
| ③ | Input | 필수 | 사용자가 텍스트를 입력하는 영역 |
| ④ | Suffix Icon / Clear | 선택 | 입력 영역 뒤 아이콘 또는 Clear 버튼 (Search variant에서 자동 표시) |
| ⑤ | Container | 필수 | 배경, 테두리를 포함하는 외곽 |
| ⑥ | Helper / Error Text | 선택 | 입력 안내 또는 에러 메시지 (에러 시 Helper를 대체) |
| ⑦ | Character Counter | 선택 | `maxLength` 지정 시 표시되는 글자 수 카운터 |

---

## 3. 옵션 (Options)

| Property | Type | Values | Default | 설명 |
|----------|------|--------|---------|------|
| `variant` | enum | `"default"` \| `"search"` | `"default"` | 시각적 변형 |
| `size` | enum | `"sm"` \| `"md"` \| `"lg"` | `"md"` | 크기 |
| `disabled` | boolean | `true` \| `false` | `false` | 비활성 상태 |
| `readOnly` | boolean | `true` \| `false` | `false` | 읽기 전용 상태 |
| `error` | boolean | `true` \| `false` | `false` | 에러 상태 |
| `label` | string | — | `undefined` | 라벨 텍스트 |
| `placeholder` | string | — | `undefined` | 플레이스홀더 텍스트 |
| `helperText` | string | — | `undefined` | 하단 도움말 텍스트 |
| `errorText` | string | — | `undefined` | 하단 에러 메시지 (`error=true` 시 `helperText` 대체) |
| `maxLength` | number | — | `undefined` | 최대 글자 수 (지정 시 카운터 표시) |
| `prefixIcon` | icon | — | `undefined` | 입력 앞 아이콘 (Search variant에서는 검색 아이콘 고정) |
| `suffixIcon` | icon | — | `undefined` | 입력 뒤 아이콘 (Search variant에서는 clear 버튼으로 대체) |

---

## 4. 인터랙션 (Interactions)

| 입력 | 동작 |
|------|------|
| **Click / Tap** (Container) | 입력 영역에 포커스, 커서 표시 |
| **Focus** | 포커스 스타일 전환 (stroke 색상 변경) |
| **Blur** | 포커스 해제, 유효성 검사 트리거 |
| **Typing** | 실시간 텍스트 입력, `maxLength` 초과 시 입력 제한 |
| **Clear 버튼** (Search variant) | 입력값 전체 삭제, 포커스 유지 |
| **Error 발생** | 에러 스타일 전환 + 짧은 수평 흔들림(shake) 애니메이션 |
| **Hover** (Web) | hover 스타일 전환 (stroke 색상 미세 변화) |
| **Disabled** | 시각적으로 흐려짐, 모든 인터랙션 무시 |
| **ReadOnly** | 텍스트 선택·복사는 가능, 편집 불가 |

---

## 5. 가이드라인 (Do & Don't)

### DO

- ✅ **모든 폼 필드에는 Label을 표시합니다** (Search variant 제외)
  ```
  이름                    ← Label
  ┌─────────────────┐
  │ 홍길동            │    ← Input
  └─────────────────┘
  ```

- ✅ **이메일, 전화번호는 인라인 유효성 검사를 수행합니다** — blur 시 즉시 피드백
  ```
  이메일
  ┌─────────────────────┐
  │ user@example         │
  └─────────────────────┘
  올바른 이메일 주소를 입력해 주세요    ← Error Text (에러 상태)
  ```

- ✅ **후기 작성 등 긴 텍스트에는 `maxLength`로 글자 수 카운터를 표시합니다**
  ```
  후기 작성
  ┌─────────────────────┐
  │ 차량 상태가 매우 좋았고… │
  └─────────────────────┘
  최소 20자 이상 작성해 주세요    128/500
  ```

- ✅ **Search variant는 검색 맥락에서만 사용합니다** — Label 없이 placeholder로 안내
  ```
  ┌──────────────────────────┐
  │ 🔍  도시, 공항, 역 검색    │  ← Search variant
  └──────────────────────────┘
  ```

- ✅ **Placeholder는 예시 값을 보여줍니다** — "입력하세요" 같은 일반 문구 대신 구체적 예시
  ```
  ✅ "예: 제주도, 김포공항"
  ❌ "검색어를 입력하세요"
  ```

### DON'T

- ❌ **Label 대신 Placeholder만으로 필드를 설명하지 않습니다** — 입력 시 안내가 사라짐
  ```
  ❌ ┌─────────────┐
     │ 이메일        │    ← placeholder만으로 안내
     └─────────────┘

  ✅ 이메일              ← Label
     ┌─────────────┐
     │ user@mail.com│    ← placeholder는 예시
     └─────────────┘
  ```

- ❌ **에러 메시지를 Placeholder에 표시하지 않습니다** — `errorText`를 사용
  ```
  ❌ ┌─────────────────────┐
     │ 이메일 형식이 잘못됨     │    ← placeholder로 에러 표시
     └─────────────────────┘

  ✅ ┌─────────────────────┐
     │ user@example         │
     └─────────────────────┘
     올바른 이메일 주소를 입력해 주세요    ← errorText
  ```

- ❌ **비밀번호 등 민감 정보에 Search variant를 사용하지 않습니다**

- ❌ **ReadOnly 상태에서 Placeholder를 표시하지 않습니다** — 항상 실제 값 표시

---

## 6. 플랫폼 차이 (Platform Differences)

| 항목 | Web | iOS | Android |
|------|-----|-----|---------|
| 구현 기반 | Custom `<input>` | `UITextField` | Material Outlined TextField |
| Hover 상태 | 지원 | 미지원 (터치) | 미지원 (터치) |
| 포커스 링 | 키보드 포커스 시 표시 | VoiceOver 포커스 | TalkBack 포커스 |
| 키보드 타입 | `inputMode` 속성 | `keyboardType` 프로퍼티 | `inputType` XML 속성 |
| Clear 버튼 (Search) | suffix 영역 커스텀 버튼 | `clearButtonMode` 네이티브 | suffix endIcon 커스텀 |
| `size="lg"` 높이 | 52px | 52pt | 52dp |
| 최소 터치 타겟 | 44px | 44pt | 48dp |
| 에러 Shake 애니메이션 | CSS animation | `CAKeyframeAnimation` | `ObjectAnimator` |

---

## 7. 접근성 (Accessibility)

| 속성 | 값 |
|------|-----|
| **Role** | `textbox` |
| **aria-label** | Label 텍스트와 동일 (Label 생략 시, 예: Search variant, 반드시 지정) |
| **aria-describedby** | helperText 또는 errorText 요소의 `id` 연결 |
| **aria-invalid** | error 상태에서 `true` |
| **aria-disabled** | disabled 상태에서 `true` |
| **aria-readonly** | readOnly 상태에서 `true` |
| **키보드** | `Tab`으로 포커스, 입력 즉시 가능 |
| **스크린 리더** | "[라벨], 텍스트 필드" 또는 "[라벨], 에러, [에러 메시지], 텍스트 필드" (에러 시) |
| **색상 외 표시** | 에러는 색상 + 아이콘 + 텍스트 메시지로 삼중 표시 |

---

## 8. Carmore 사용 예시

### 로그인 / 회원가입

```
이메일
┌───────────────────────────────┐
│ carmore@example.com            │
└───────────────────────────────┘

비밀번호
┌───────────────────────────────┐
│ ••••••••              [👁]    │  ← suffixIcon: 비밀번호 표시 토글
└───────────────────────────────┘

┌───────────────────────────────┐
│         로그인                 │  ← Button (primary, lg, fill)
└───────────────────────────────┘
```

### 메인 검색 바

```
┌───────────────────────────────┐
│ 🔍  제주도, 김포공항, 서울역    │  ← TextField (variant="search", lg)
└───────────────────────────────┘
```

### 예약자 정보 입력

```
이름 *                             전화번호 *
┌──────────────┐                  ┌──────────────┐
│ 홍길동         │                  │ 010-1234-5678 │
└──────────────┘                  └──────────────┘

이메일 *
┌───────────────────────────────┐
│ user@example                   │
└───────────────────────────────┘
올바른 이메일 주소를 입력해 주세요    ← errorText
```
