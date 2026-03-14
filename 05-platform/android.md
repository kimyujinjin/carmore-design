# Android Platform Guide

> Edge-to-edge, Material 3 정렬, 네이티브 컴포넌트 매핑, Compose 토큰 사용

---

## 1. Material 3 정렬

Carmore Design System은 Material 3를 기반으로 하되, **브랜드 토큰을 우선 적용**합니다.

### Material 3와의 관계

| 항목 | Material 3 기본 | Carmore 적용 |
|------|----------------|-------------|
| Dynamic Color | Material You 동적 색상 | **사용하지 않음** — 브랜드 토큰 고정 |
| Shape | 3단계 (Small/Medium/Large) | Carmore Radius 토큰 매핑 |
| Typography | Material Type Scale | Carmore Type Scale 사용 |
| Motion | Material Motion | Carmore Motion 토큰 사용 |
| Elevation | Material Elevation | Carmore Elevation 매핑 |

### Shape 매핑

| Carmore Radius | Material 3 Shape | Value |
|---------------|------------------|-------|
| `$radius.sm` | ShapeDefaults.Small | 8dp |
| `$radius.md` | ShapeDefaults.Medium | 12dp |
| `$radius.lg` | ShapeDefaults.Large | 16dp |
| `$radius.xl` | ShapeDefaults.ExtraLarge | 20dp |
| `$radius.full` | CircleShape | pill |

---

## 2. Edge-to-Edge 대응

Android 15+ 에서는 Edge-to-Edge가 기본 적용됩니다.

### 시스템 바 처리

```
┌─ Status Bar (투명) ─────────────┐
│  ← 시스템 아이콘 오버레이         │
├──────────────────────────────────┤
│                                  │
│          Content Area            │  ← WindowInsets 적용
│                                  │
├──────────────────────────────────┤
│  ← Navigation Bar (투명)         │
│     제스처 네비게이션 또는 3버튼   │
└──────────────────────────────────┘
```

### Compose 구현

```kotlin
@Composable
fun CarmoreScreen() {
    Scaffold(
        modifier = Modifier.fillMaxSize(),
        contentWindowInsets = WindowInsets.systemBars,
    ) { innerPadding ->
        Content(
            modifier = Modifier.padding(innerPadding)
        )
    }
}
```

### Sticky CTA 버튼 처리

```kotlin
@Composable
fun StickyCtaButton() {
    val navBarInsets = WindowInsets.navigationBars

    Box(
        modifier = Modifier
            .fillMaxWidth()
            .windowInsetsPadding(navBarInsets)
            .padding(
                horizontal = CarmoreSpacing.x4,  // 16dp
                vertical = CarmoreSpacing.x3      // 12dp
            )
    ) {
        CarmoreButton(
            variant = ButtonVariant.Primary,
            size = ButtonSize.Large,
            modifier = Modifier.fillMaxWidth()
        )
    }
}
```

---

## 3. 네이티브 컴포넌트 매핑

| Carmore 컴포넌트 | Android 구현 | 비고 |
|-----------------|-------------|------|
| **Button** | Compose `Button` 커스텀 | CarmoreButton composable |
| **TextField** | Compose `OutlinedTextField` 커스텀 | CarmoreTextField composable |
| **Card** | Compose `Card` 커스텀 | CarmoreCard composable |
| **BottomSheet** | `ModalBottomSheet` | Material 3 + 커스텀 콘텐츠 |
| **Dialog** | `AlertDialog` 커스텀 | CarmoreDialog composable |
| **FilterChip** | `FilterChip` (Material 3) | 색상/형태만 커스텀 |
| **ComparisonTable** | `LazyRow` + `LazyColumn` | 완전 커스텀 |
| **Navigation** | Navigation Component | Jetpack Navigation |
| **Tab/Bottom Nav** | `NavigationBar` | Material 3 + 커스텀 색상 |

### BottomSheet 분기

| 상황 | 구현 |
|------|------|
| modal (스크림 있음) | `ModalBottomSheet` |
| persistent (스크림 없음) | `BottomSheetScaffold` |

```kotlin
ModalBottomSheet(
    onDismissRequest = { /* dismiss */ },
    sheetState = rememberModalBottomSheetState(),
    shape = RoundedCornerShape(
        topStart = CarmoreRadius.lg,  // 16dp
        topEnd = CarmoreRadius.lg
    ),
    containerColor = CarmoreColors.bgNeutral,
    dragHandle = { BottomSheetDefaults.DragHandle() },
    scrimColor = CarmoreColors.bgOverlay,
) {
    // Sheet content
}
```

---

## 4. Compose Theme 토큰

### Colors

```kotlin
object CarmoreColors {
    // Brand
    val bgBrand = Color(0xFF0077ED)
    val bgBrandHover = Color(0xFF005FBE)
    val bgBrandPressed = Color(0xFF00478E)
    val bgBrandWeak = Color(0xFFEBF5FF)

    // Accent
    val bgAccent = Color(0xFFFFB314)
    val fgAccent = Color(0xFF805600)

    // Neutral
    val bgNeutral = Color(0xFFFFFFFF)
    val bgNeutralWeak = Color(0xFFF7F8FA)
    val bgNeutralHover = Color(0xFFF0F1F3)
    val fgNeutral = Color(0xFF1F2430)
    val fgNeutralWeak = Color(0xFF6B7280)
    val fgNeutralWeakest = Color(0xFFAEB3BC)
    val fgOnBrand = Color(0xFFFFFFFF)

    // Semantic
    val bgPositive = Color(0xFF16A34A)
    val bgPositiveWeak = Color(0xFFDCFCE7)
    val fgPositive = Color(0xFF16A34A)
    val bgCritical = Color(0xFFDC2626)
    val bgCriticalWeak = Color(0xFFFEE2E2)
    val fgCritical = Color(0xFFDC2626)
    val bgWarningWeak = Color(0xFFFEF9C3)
    val fgWarning = Color(0xFFA16207)

    // Stroke
    val strokeNeutral = Color(0xFFE4E6E9)
    val strokeNeutralStrong = Color(0xFFCBCED4)
    val strokeBrand = Color(0xFF0077ED)
    val strokeCritical = Color(0xFFDC2626)

    // Disabled
    val bgDisabled = Color(0xFFF0F1F3)
    val fgDisabled = Color(0xFFCBCED4)

    // Overlay
    val bgOverlay = Color(0x66000000)  // 40% black
}
```

### Typography

```kotlin
object CarmoreTypography {
    private val pretendard = FontFamily(
        Font(R.font.pretendard_regular, FontWeight.Normal),
        Font(R.font.pretendard_medium, FontWeight.Medium),
        Font(R.font.pretendard_bold, FontWeight.Bold),
    )

    val title1 = TextStyle(
        fontFamily = pretendard, fontSize = 28.sp,
        fontWeight = FontWeight.Bold, lineHeight = 36.sp
    )
    val title2 = TextStyle(
        fontFamily = pretendard, fontSize = 24.sp,
        fontWeight = FontWeight.Bold, lineHeight = 32.sp
    )
    val title3 = TextStyle(
        fontFamily = pretendard, fontSize = 20.sp,
        fontWeight = FontWeight.Bold, lineHeight = 28.sp
    )
    val subtitle1 = TextStyle(
        fontFamily = pretendard, fontSize = 18.sp,
        fontWeight = FontWeight.Medium, lineHeight = 26.sp
    )
    val body1 = TextStyle(
        fontFamily = pretendard, fontSize = 16.sp,
        fontWeight = FontWeight.Normal, lineHeight = 24.sp
    )
    val body2 = TextStyle(
        fontFamily = pretendard, fontSize = 14.sp,
        fontWeight = FontWeight.Normal, lineHeight = 20.sp
    )
    val caption1 = TextStyle(
        fontFamily = pretendard, fontSize = 13.sp,
        fontWeight = FontWeight.Normal, lineHeight = 18.sp
    )
    val label1 = TextStyle(
        fontFamily = pretendard, fontSize = 16.sp,
        fontWeight = FontWeight.Bold, lineHeight = 24.sp
    )
    val label2 = TextStyle(
        fontFamily = pretendard, fontSize = 14.sp,
        fontWeight = FontWeight.Bold, lineHeight = 20.sp
    )
    val price = TextStyle(
        fontFamily = pretendard, fontSize = 16.sp,
        fontWeight = FontWeight.Bold, lineHeight = 24.sp
    )
}
```

### Spacing & Radius

```kotlin
object CarmoreSpacing {
    val x0_5 = 2.dp
    val x1 = 4.dp
    val x1_5 = 6.dp
    val x2 = 8.dp
    val x3 = 12.dp
    val x4 = 16.dp
    val x5 = 20.dp
    val x6 = 24.dp
    val x8 = 32.dp
    val x10 = 40.dp
}

object CarmoreRadius {
    val sm = 8.dp
    val md = 12.dp
    val lg = 16.dp
    val xl = 20.dp
    val full = 9999.dp
}
```

---

## 5. Predictive Back (제스처 뒤로가기)

Android 14+ 에서는 Predictive Back 애니메이션을 지원합니다.

### 대응 컴포넌트

| 컴포넌트 | 뒤로가기 동작 |
|----------|-------------|
| BottomSheet | 스와이프 다운으로 닫기 (Predictive Back 자동 지원) |
| Dialog | 뒤로가기 시 닫기 (dismissible=true) |
| 검색 화면 | 뒤로가기 시 이전 화면 복귀 |
| 폼 입력 중 | 뒤로가기 시 이탈 방지 Dialog 표시 |

```kotlin
// Predictive Back 대응
BackHandler(enabled = showSheet) {
    scope.launch { sheetState.hide() }
}
```

---

## 6. 터치 타겟

Material Design Guidelines에 따라:

| 요소 | 최소 크기 | 비고 |
|------|-----------|------|
| 버튼, 탭 가능 요소 | 48 × 48dp | Material 권장 |
| 리스트 행 | 높이 56dp | Material 표준 행 |
| 아이콘 버튼 | 아이콘 24dp + 패딩 = 48dp | 터치 영역 확장 |

```kotlin
IconButton(
    onClick = { /* ... */ },
    modifier = Modifier.size(48.dp)  // 최소 터치 타겟
) {
    Icon(
        imageVector = Icons.Default.Search,
        contentDescription = "검색",
        modifier = Modifier.size(24.dp)
    )
}
```

---

## 7. 접근성 (Android 고유)

| 항목 | 구현 |
|------|------|
| TalkBack | `contentDescription` 필수 지정 |
| 크기 조정 | `sp` 단위로 사용자 글꼴 크기 설정 존중 |
| 색상 반전 | 시맨틱 토큰 사용으로 자동 대응 |
| Switch Access | 포커스 순서 `focusOrder` 지정 |
| 터치 탐색 | `semantics` 블록으로 요소 그룹화 |

```kotlin
Card(
    modifier = Modifier.semantics(mergeDescendants = true) {
        contentDescription = "현대 아반떼, 서울 강남, 1일 45,000원, 평점 4.8"
    }
) {
    // Card content
}
```
