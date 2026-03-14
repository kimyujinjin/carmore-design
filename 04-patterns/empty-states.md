# Empty States (빈 화면 패턴)

> 콘텐츠가 없거나 에러가 발생했을 때의 화면 처리 패턴

---

## 개요

Empty State는 사용자에게 **현재 상황을 설명하고, 다음 행동을 안내**하는 화면입니다. 단순히 "데이터 없음"을 표시하는 것이 아니라, 상황에 맞는 안내와 행동 유도(CTA)를 제공해야 합니다.

---

## 기본 구조

```
┌─────────────────────────────────┐
│                                 │
│          ① Illustration         │  ← $icon.xl (48px) 또는 일러스트
│                                 │
│        ② Title                  │  ← $typography.title3
│        ③ Description            │  ← $typography.body1
│                                 │
│        ④ [CTA Button]           │  ← Button (선택)
│                                 │
└─────────────────────────────────┘
```

| # | 요소 | 필수 | 설명 |
|---|------|------|------|
| ① | Illustration / Icon | 필수 | 상황을 시각적으로 전달하는 아이콘 또는 일러스트 |
| ② | Title | 필수 | 현재 상태를 한 문장으로 설명 |
| ③ | Description | 선택 | 추가 설명 또는 해결 방법 안내 |
| ④ | CTA Button | 선택 | 다음 행동을 유도하는 버튼 |

### 레이아웃 토큰

| 요소 | 간격 |
|------|------|
| Icon → Title | `$dimension.x4` (16px) |
| Title → Description | `$dimension.x2` (8px) |
| Description → CTA | `$dimension.x6` (24px) |
| 전체 컨테이너 | 수직/수평 중앙 정렬 |
| 좌우 여백 | `$dimension.x10` (40px) 이상 |

---

## 유형별 Empty State

### 1. 검색 결과 없음

```
        🔍
   검색 결과가 없습니다

   "서울 강남"에서 조건에 맞는
   렌터카를 찾지 못했습니다.
   필터를 조정해 보세요.

   [필터 초기화]  ← Button(secondary, md)
```

| 항목 | 값 |
|------|-----|
| Icon | `ic_action_search` (`$color.fg.neutral-weak`) |
| Title | "검색 결과가 없습니다" |
| Description | 검색 조건을 포함한 안내 |
| CTA | "필터 초기화" (Button, secondary) |

### 2. 예약 내역 없음

```
        📋
   아직 예약 내역이 없습니다

   첫 여행을 계획해 보세요!
   렌터카와 숙박을 한 번에 예약할 수 있습니다.

   [여행지 검색하기]  ← Button(primary, md)
```

| 항목 | 값 |
|------|-----|
| Icon | `ic_booking_receipt` (`$color.fg.neutral-weak`) |
| Title | "아직 예약 내역이 없습니다" |
| Description | 서비스 가치를 전달하는 안내 |
| CTA | "여행지 검색하기" (Button, primary) |

### 3. 찜 목록 없음

```
        ♡
   저장한 숙소가 없습니다

   마음에 드는 숙소에 ♡를 눌러
   나중에 쉽게 찾아보세요.

   [숙소 둘러보기]  ← Button(primary, md)
```

### 4. 네트워크 에러

```
        ⚠️
   연결에 문제가 있습니다

   인터넷 연결을 확인하고
   다시 시도해 주세요.

   [다시 시도]  ← Button(primary, md)
```

| 항목 | 값 |
|------|-----|
| Icon | `ic_status_warning` (`$color.fg.warning`) |
| Title | "연결에 문제가 있습니다" |
| CTA | "다시 시도" — 재시도 액션 |

### 5. 서버 에러

```
        ❗
   일시적인 문제가 발생했습니다

   잠시 후 다시 시도해 주세요.
   문제가 계속되면 고객센터에 문의해 주세요.

   [다시 시도]        [고객센터]
   Button(primary)    Button(secondary)
```

### 6. 권한 필요

```
        🔒
   로그인이 필요합니다

   예약 내역을 확인하려면
   로그인해 주세요.

   [로그인]  ← Button(primary, md)
```

---

## 스타일 가이드

### 색상

| 요소 | Token | 비고 |
|------|-------|------|
| Icon (일반) | `$color.fg.neutral-weak` | 중립적 톤 |
| Icon (에러) | `$color.fg.warning` 또는 `$color.fg.critical` | 문제 상황 |
| Title | `$color.fg.neutral` | 기본 텍스트 |
| Description | `$color.fg.neutral-weak` | 보조 텍스트 |

### 타이포그래피

| 요소 | Token |
|------|-------|
| Title | `$typography.title3` (t3Bold, 20px) |
| Description | `$typography.body1` (t5Regular, 16px) |

---

## Do & Don't

### DO

- ✅ Title에 **현재 상태**를 명확히 설명합니다
- ✅ Description에 **해결 방법 또는 다음 행동**을 안내합니다
- ✅ CTA 버튼으로 사용자를 다음 단계로 유도합니다
- ✅ 긍정적이고 격려하는 톤을 사용합니다 ("아직 ~ 없습니다" > "~ 없음")

### DON'T

- ❌ 기술적 에러 코드를 사용자에게 노출하지 않습니다 ("Error 500" → "일시적인 문제가 발생했습니다")
- ❌ 빈 화면을 그대로 두지 않습니다 (최소한 아이콘 + 텍스트)
- ❌ CTA 없이 막다른 길을 만들지 않습니다
- ❌ 부정적이거나 비난하는 톤을 사용하지 않습니다 ("잘못된 입력" → "조건을 조정해 보세요")
