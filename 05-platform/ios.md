# iOS Platform Guide

> Safe Area, SF Symbols, 네이티브 컴포넌트 매핑, Swift 토큰 사용

---

## 1. Human Interface Guidelines 정렬

Carmore Design System은 Apple HIG를 존중하면서 브랜드 정체성을 유지합니다.

### 존중하는 네이티브 관습

| HIG 원칙 | Carmore 적용 |
|----------|-------------|
| Safe Area | 콘텐츠는 Safe Area 내에만 배치, 배경색은 전체 적용 |
| Dynamic Type | 텍스트 크기 접근성 설정 존중 |
| 스와이프 백 | 네이티브 edge swipe back 유지 |
| 시스템 폰트 | SF Pro 사용 (Pretendard 대신) |
| 햅틱 피드백 | 버튼 탭, 토글, 삭제 시 UIImpactFeedbackGenerator |

### Carmore 고유 스타일 유지

| 항목 | HIG 기본 | Carmore 적용 |
|------|---------|-------------|
| 버튼 모양 | 시스템 tinted/gray | 커스텀 shape + 브랜드 토큰 |
| 카드 스타일 | 기본 제공 없음 | 커스텀 Card 컴포넌트 |
| 색상 | 시스템 AccentColor | `$color.bg.brand` (#0077ED) |
| BottomSheet | UISheetPresentationController | 네이티브 위에 커스텀 콘텐츠 |

---

## 2. Safe Area 처리

### 일반 화면

```
┌─ Status Bar ────────────────────┐
│          (Safe Area Top)         │
├──────────────────────────────────┤
│                                  │
│          Content Area            │  ← Safe Area 내부
│                                  │
├──────────────────────────────────┤
│       (Safe Area Bottom)         │
├──────────────────────────────────┤
│       Home Indicator             │
└──────────────────────────────────┘
```

### Sticky CTA 버튼

```
┌──────────────────────────────────┐
│  스크롤 콘텐츠                    │
│  ...                             │
├──────────────────────────────────┤
│  ┌────────────────────────┐     │
│  │   ₩150,000 결제하기    │     │  ← Button(primary, lg, fill)
│  └────────────────────────┘     │
│  padding-bottom:                 │
│  $dimension.x4 + safeAreaBottom  │  ← Safe Area 추가 여백
├──────────────────────────────────┤
│  Home Indicator                  │
└──────────────────────────────────┘
```

### BottomSheet

```swift
if let sheet = viewController.sheetPresentationController {
    sheet.detents = [.medium(), .large()]
    sheet.prefersGrabberVisible = true
    sheet.preferredCornerRadius = 16  // $radius.lg
}
```

- BottomSheet 상단 radius: `$radius.lg` (16pt)
- Sheet 내부 콘텐츠는 Safe Area 자동 존중
- `medium()` detent = 화면 절반, `large()` = 거의 전체

---

## 3. 네이티브 컴포넌트 매핑

| Carmore 컴포넌트 | iOS 네이티브 | 구현 방식 |
|-----------------|-------------|-----------|
| **Button** | UIButton | 커스텀 UIButton 서브클래스 |
| **TextField** | UITextField | 커스텀 뷰 (라벨+필드+헬퍼 묶음) |
| **Card** | UIView | 커스텀 UIView |
| **BottomSheet** | UISheetPresentationController | 네이티브 + 커스텀 콘텐츠 |
| **Dialog** | UIAlertController (alert) | 커스텀 뷰 (confirm/destructive variant) |
| **FilterChip** | UIButton (toggle) | 커스텀 UICollectionView + UIButton |
| **ComparisonTable** | UICollectionView | 커스텀 Compositional Layout |
| **Navigation** | UINavigationController | 네이티브 |
| **Tab Bar** | UITabBarController | 네이티브 + 커스텀 색상 |

### Dialog 분기

| Variant | iOS 구현 |
|---------|---------|
| `alert` | `UIAlertController(.alert)` — 네이티브 사용 가능 |
| `confirm` | 커스텀 뷰 (브랜드 스타일 적용) |
| `destructive` | 커스텀 뷰 (빨간 버튼 + 포커스 규칙) |

---

## 4. SF Symbols 매핑

표준 아이콘은 SF Symbols를 사용하고, 도메인 전용 아이콘만 커스텀 SVG를 사용합니다.

### 기본 아이콘 → SF Symbols

| Carmore Icon | SF Symbol | Weight |
|-------------|-----------|--------|
| `ic_nav_back` | `chevron.left` | medium |
| `ic_nav_close` | `xmark` | medium |
| `ic_action_search` | `magnifyingglass` | medium |
| `ic_action_filter` | `line.3.horizontal.decrease` | medium |
| `ic_action_share` | `square.and.arrow.up` | medium |
| `ic_booking_calendar` | `calendar` | medium |
| `ic_booking_clock` | `clock` | medium |
| `ic_general_star` | `star` / `star.fill` | medium |
| `ic_general_heart` | `heart` / `heart.fill` | medium |
| `ic_general_location` | `location` | medium |
| `ic_general_phone` | `phone` | medium |
| `ic_status_check` | `checkmark.circle` / `.fill` | medium |
| `ic_status_warning` | `exclamationmark.triangle` | medium |
| `ic_status_error` | `exclamationmark.circle` | medium |
| `ic_status_info` | `info.circle` | medium |

### 커스텀 아이콘 (SF Symbol 대체 불가)

| Carmore Icon | 설명 |
|-------------|------|
| `ic_vehicle_sedan` | 세단 차량 실루엣 |
| `ic_vehicle_suv` | SUV 차량 실루엣 |
| `ic_vehicle_van` | 밴 차량 실루엣 |
| `ic_accom_hotel` | 호텔 건물 |
| `ic_accom_villa` | 빌라/펜션 |
| `ic_booking_receipt` | 영수증/예약증 |

> 커스텀 아이콘은 SF Symbols와 동일한 weight/optical size 기준으로 제작합니다.

---

## 5. Swift 토큰 사용

### 색상

```swift
extension UIColor {
    struct Carmore {
        // Semantic
        static let bgBrand = UIColor(hex: "#0077ED")
        static let bgBrandHover = UIColor(hex: "#005FBE")
        static let fgNeutral = UIColor(hex: "#1F2430")
        static let fgNeutralWeak = UIColor(hex: "#6B7280")
        static let fgOnBrand = UIColor(hex: "#FFFFFF")
        static let fgCritical = UIColor(hex: "#DC2626")
        static let strokeNeutral = UIColor(hex: "#E4E6E9")
        static let strokeBrand = UIColor(hex: "#0077ED")
        static let bgOverlay = UIColor.black.withAlphaComponent(0.4)
        // ... 기타 토큰
    }
}
```

### 타이포그래피

```swift
extension UIFont {
    struct Carmore {
        static let title1 = UIFont.systemFont(ofSize: 28, weight: .bold)
        static let title2 = UIFont.systemFont(ofSize: 24, weight: .bold)
        static let title3 = UIFont.systemFont(ofSize: 20, weight: .bold)
        static let subtitle1 = UIFont.systemFont(ofSize: 18, weight: .medium)
        static let body1 = UIFont.systemFont(ofSize: 16, weight: .regular)
        static let body2 = UIFont.systemFont(ofSize: 14, weight: .regular)
        static let caption1 = UIFont.systemFont(ofSize: 13, weight: .regular)
        static let label1 = UIFont.systemFont(ofSize: 16, weight: .bold)
        static let label2 = UIFont.systemFont(ofSize: 14, weight: .bold)
    }
}
```

### 간격 / 곡률

```swift
struct CarmoreSpacing {
    static let x1: CGFloat = 4
    static let x2: CGFloat = 8
    static let x3: CGFloat = 12
    static let x4: CGFloat = 16
    static let x6: CGFloat = 24
    static let x8: CGFloat = 32
}

struct CarmoreRadius {
    static let sm: CGFloat = 8
    static let md: CGFloat = 12
    static let lg: CGFloat = 16
    static let xl: CGFloat = 20
    static let full: CGFloat = 9999
}
```

---

## 6. Dynamic Type 지원

```swift
label.font = UIFontMetrics(forTextStyle: .body)
    .scaledFont(for: Carmore.body1)
label.adjustsFontForContentSizeCategory = true
```

| Carmore Token | UIFont.TextStyle |
|---------------|-----------------|
| `$typography.title1` | `.title1` |
| `$typography.title2` | `.title2` |
| `$typography.title3` | `.title3` |
| `$typography.body1` | `.body` |
| `$typography.body2` | `.subheadline` |
| `$typography.caption1` | `.caption1` |
| `$typography.label1` | `.body` (bold) |

---

## 7. 터치 타겟

iOS Human Interface Guidelines에 따라:

| 요소 | 최소 크기 | 비고 |
|------|-----------|------|
| 버튼, 탭 가능 요소 | 44 × 44pt | HIG 권장 |
| 리스트 행 | 높이 44pt 이상 | 표준 행 높이 |
| 아이콘 버튼 | 아이콘 24pt + 패딩 = 44pt | 터치 영역 확장 |

---

## 8. 햅틱 피드백

| 인터랙션 | 햅틱 타입 |
|---------|-----------|
| 버튼 탭 | `UIImpactFeedbackGenerator(.light)` |
| 토글/칩 선택 | `UIImpactFeedbackGenerator(.light)` |
| 파괴적 액션 확인 | `UINotificationFeedbackGenerator(.warning)` |
| 예약 성공 | `UINotificationFeedbackGenerator(.success)` |
| 에러 | `UINotificationFeedbackGenerator(.error)` |
| BottomSheet snap | `UIImpactFeedbackGenerator(.medium)` |
