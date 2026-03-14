# Form Input (폼 입력 패턴)

> 텍스트 입력, 유효성 검사, 에러 처리를 위한 UI/UX 패턴

---

## 개요

Carmore에서 폼 입력은 예약자 정보(이름, 이메일, 연락처), 결제 정보, 리뷰 작성 등에 사용됩니다. 올바른 데이터를 쉽고 빠르게 수집하면서 사용자의 실수를 최소화하는 것이 목표입니다.

---

## 1. 폼 필드 해부도

```
┌─ Label ─────────────────────────┐
│  이름 *                         │  ← $typography.caption1 (t8Medium)
├─────────────────────────────────┤
│  ┌─────────────────────────┐   │
│  │  ① Prefix  ② Input  ③ │   │  ← TextField
│  └─────────────────────────┘   │
├─────────────────────────────────┤
│  ④ Helper / Error Text          │  ← $typography.caption1 (t8Regular)
│  ⑤ Character Counter (선택)     │  ← 우측 정렬
└─────────────────────────────────┘
```

| # | 요소 | 필수 | 토큰 |
|---|------|------|------|
| Label | 필드명 + 필수 표시(*) | 필수 | `$color.fg.neutral` / `$typography.caption1` |
| Prefix | 아이콘 또는 텍스트 (국가번호 등) | 선택 | `$color.fg.neutral-weak` |
| Input | 사용자 입력 텍스트 | 필수 | `$color.fg.neutral` / placeholder: `$color.fg.neutral-weakest` |
| Suffix | 클리어 버튼, 유효성 아이콘 | 선택 | `$color.fg.neutral-weak` |
| Helper Text | 입력 안내, 포맷 예시 | 선택 | `$color.fg.neutral-weak` |
| Error Text | 유효성 오류 메시지 | 조건부 | `$color.fg.critical` |
| Character Counter | 잔여 글자 수 | 선택 | `$color.fg.neutral-weak` |

---

## 2. 필수 vs 선택 표시

### 방식: 필수 항목에 * 표시

```
이름 *               ← 필수
이메일 *             ← 필수
특별 요청 (선택)     ← 선택일 때만 "(선택)" 표기
```

- 대부분이 필수일 때: 필수에 `*` 표시
- 대부분이 선택일 때: 선택에 `(선택)` 표시
- `*` 색상: `$color.fg.critical`

---

## 3. 유효성 검사 전략

### 검증 시점

| 전략 | 시점 | 사용 케이스 |
|------|------|------------|
| **On Blur** | 필드에서 포커스가 벗어날 때 | 이메일, 이름 등 대부분의 필드 |
| **On Change** (실시간) | 값이 변경될 때 즉시 | 전화번호 포맷, 글자 수 카운터 |
| **On Submit** | 폼 제출 시 | 서버 측 검증 (중복 이메일 등) |

### 에러 표시 규칙

```
1. 에러 상태 활성화
   - TextField stroke → $color.stroke.critical
   - Helper text → Error text로 교체 (색상: $color.fg.critical)
   - Error icon (ic_status_error) 표시 (suffix 위치)

2. 에러 해제 조건
   - 사용자가 필드를 수정하면 즉시 에러 표시 해제
   - 다시 blur 시 재검증

3. 에러 포커스
   - 제출 시 에러가 있으면 첫 번째 에러 필드로 자동 스크롤 + 포커스
```

### 필드별 유효성 규칙

| 필드 | 규칙 | 에러 메시지 | 검증 시점 |
|------|------|------------|-----------|
| 이름 | 2자 이상, 특수문자 금지 | "이름을 2자 이상 입력해 주세요" | blur |
| 이메일 | RFC 5322 형식 | "올바른 이메일 주소를 입력해 주세요" | blur |
| 전화번호 | 숫자 + 하이픈, 10~11자 | "올바른 연락처를 입력해 주세요" | blur |
| 운전면허 | 국가별 형식 | "올바른 면허번호를 입력해 주세요" | blur |
| 리뷰 | 10자 이상, 500자 이하 | "10자 이상 작성해 주세요" | blur + counter |

---

## 4. 입력 포맷팅

### 자동 포맷 적용 필드

| 필드 | 입력 | 표시 |
|------|------|------|
| 전화번호 | `01012345678` | `010-1234-5678` |
| 카드번호 | `1234567890123456` | `1234 5678 9012 3456` |
| 유효기간 | `0328` | `03/28` |
| 금액 | `150000` | `₩150,000` |

### 규칙

- 자동 포맷은 **표시만** 변경하고, 실제 입력 값은 원본 유지
- 포맷 적용 중에도 커서 위치를 올바르게 유지

---

## 5. 키보드 타입 (모바일)

| 필드 | iOS keyboardType | Android inputType |
|------|-----------------|-------------------|
| 이름 | `.default` | `textPersonName` |
| 이메일 | `.emailAddress` | `textEmailAddress` |
| 전화번호 | `.phonePad` | `phone` |
| 카드번호 | `.numberPad` | `number` |
| 금액 | `.decimalPad` | `numberDecimal` |
| URL | `.URL` | `textUri` |

---

## 6. 폼 레이아웃

### 간격 규칙

```
┌─────────────────────────────────┐
│  [섹션 제목]                     │  ← $typography.title3
│  ← 12px →                       │  ← section-title-to-content
│  [Label]                        │
│  ← 6px →                        │  ← label-to-field
│  [TextField]                    │
│  ← 4px →                        │  ← field-to-helper
│  [Helper Text]                  │
│  ← 16px →                       │  ← component-gap-wide (필드 간)
│  [Label]                        │
│  ← 6px →                        │
│  [TextField]                    │
│  ← 24px →                       │  ← section-gap (섹션 간)
│  [다음 섹션 제목]                │
└─────────────────────────────────┘
```

### 가로 배치 (2열)

데스크톱에서 관련 필드를 가로로 배치할 수 있습니다.

```
[이름 *              ]  ← 16px gap →  [성 *               ]
[이메일 *                                                  ]
[전화번호 *          ]  ← 16px gap →  [생년월일            ]
```

- 가로 배치 간격: `$dimension.x4` (16px)
- 모바일에서는 **항상 1열** (세로 스택)

---

## 7. 접근성

| 요구사항 | 구현 |
|---------|------|
| 라벨-필드 연결 | `<label for="field-id">` 또는 `aria-labelledby` |
| 에러 연결 | `aria-describedby="error-id"` |
| 필수 표시 | `aria-required="true"` |
| 에러 상태 | `aria-invalid="true"` |
| 에러 알림 | `role="alert"` + `aria-live="polite"` |
| 탭 순서 | 시각적 순서와 일치하는 `tabindex` |
| 자동완성 | `autocomplete` 속성 적용 (`name`, `email`, `tel`) |

---

## 8. Do & Don't

### DO

- ✅ 모든 필드에 라벨을 표시합니다 (placeholder만으로 대체하지 않음)
- ✅ 에러 메시지에 **해결 방법**을 포함합니다 ("올바른 이메일 형식: example@mail.com")
- ✅ 긴 폼은 섹션으로 나누고 진행 표시를 제공합니다
- ✅ 입력 완료 후 다음 필드로 자동 포커스 이동 (전화번호 → 이메일)

### DON'T

- ❌ placeholder를 라벨 대용으로 사용하지 않습니다 (입력 시 사라짐)
- ❌ 제출 전에 모든 에러를 한꺼번에 표시하지 않습니다 (blur 시 개별 표시)
- ❌ 에러 메시지에 기술 용어를 사용하지 않습니다 ("RFC 5322 위반" → "올바른 이메일 주소를 입력해 주세요")
- ❌ 유효성 통과 시 초록색 체크 표시를 남발하지 않습니다 (핵심 필드에만 적용)
