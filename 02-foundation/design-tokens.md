# Design Tokens

> 디자인 시스템의 모든 시각적 속성을 정의하는 토큰 아키텍처

---

## 토큰이란?

디자인 토큰은 색상, 간격, 타이포그래피 등 시각적 속성의 **이름 붙여진 값**입니다. 하드코딩된 `#0077ED`나 `16px` 대신 `$color.bg.brand`나 `$dimension.x4`를 사용함으로써:

- **일관성**: 같은 의도를 가진 곳에 같은 값이 적용됩니다
- **유지보수**: 토큰 값 하나를 바꾸면 사용처 전체에 반영됩니다
- **커뮤니케이션**: PO, 디자이너, 개발자가 같은 이름으로 소통합니다
- **테마 지원**: 다크 모드 등 테마 전환 시 Semantic 레이어만 교체합니다

---

## 3단계 토큰 아키텍처

Carmore Design System은 SEED 디자인 시스템의 접근 방식을 참고하여 **3단계 계층 구조**를 사용합니다.

```
┌──────────────────────────────────────────────────────┐
│  Level 3: Semantic Token (의미론적 토큰)               │
│  $color.bg.brand, $color.fg.critical                  │
│  → 컴포넌트와 화면에서 직접 참조하는 토큰                │
├──────────────────────────────────────────────────────┤
│  Level 2: Scale Token (스케일 토큰)                    │
│  $color.palette.blue-500, $dimension.x4               │
│  → Raw Value에 이름을 부여한 팔레트/스케일 단위          │
├──────────────────────────────────────────────────────┤
│  Level 1: Raw Value (원시 값)                          │
│  #0077ED, 16px, 700                                   │
│  → 실제 렌더링되는 물리적 값                             │
└──────────────────────────────────────────────────────┘
```

### Level 1: Raw Value (원시 값)

실제 화면에 렌더링되는 물리적 값입니다. 문서나 코드에서 **직접 사용하지 않습니다**.

```
#0077ED    ← 색상 hex 코드
16px       ← 치수
700        ← 폰트 굵기
150ms      ← 애니메이션 시간
```

### Level 2: Scale Token (스케일 토큰)

Raw Value에 **체계적인 이름**을 부여한 팔레트 단위입니다. 값의 크기나 순서를 나타내며, 토큰 시스템의 기초 재료입니다.

```
$color.palette.blue-500      → #0077ED
$color.palette.gray-600      → #6B7280
$dimension.x4                → 16px
$radius.md                   → 12px
```

**Scale Token은 Foundation 문서에서 정의하지만, 컴포넌트에서 직접 참조하지 않습니다.** 반드시 Semantic Token을 통해 사용합니다.

### Level 3: Semantic Token (의미론적 토큰)

Scale Token을 **역할과 의도**에 맞게 매핑한 최종 토큰입니다. 컴포넌트와 화면에서 **이 레벨만 참조**합니다.

```
$color.bg.brand              → $color.palette.blue-500 → #0077ED
$color.fg.neutral            → $color.palette.gray-900 → #1F2430
$dimension.spacing.card-padding → $dimension.x4        → 16px
$typography.body1             → t5Regular               → 16px/400
```

---

## 네이밍 컨벤션

### 공통 규칙

- **점(.) 구분자**: 계층을 나타냅니다 `$color.bg.brand`
- **하이픈(-) 구분자**: 같은 레벨 내 변형을 나타냅니다 `brand-weak`, `blue-500`
- **소문자와 하이픈**: 모든 토큰명은 소문자와 하이픈만 사용합니다
- **접두사 `$`**: 토큰임을 나타내는 표기입니다

### 카테고리별 네이밍 패턴

| 카테고리 | 패턴 | 예시 |
|----------|------|------|
| **Color (Scale)** | `$color.palette.[hue]-[step]` | `$color.palette.blue-500` |
| **Color (Semantic)** | `$color.[property].[role]-[variant]` | `$color.bg.brand-weak` |
| **Dimension** | `$dimension.x{N}` | `$dimension.x4` |
| **Spacing** | `$dimension.spacing-[axis].[purpose]` | `$dimension.spacing-x.page-margin` |
| **Radius** | `$radius.[size]` | `$radius.md` |
| **Elevation** | `$elevation.[level]` | `$elevation.low` |
| **Typography** | `t{N}{Weight}` (스케일) / `$typography.[role]` (시맨틱) | `t5Medium` / `$typography.body1` |
| **Motion** | `$motion.[property].[value]` | `$motion.duration.fast` |

### Color 속성(property) 분류

| 속성 | 약어 | 용도 |
|------|------|------|
| Foreground | `fg` | 텍스트, 아이콘 색상 |
| Background | `bg` | 배경, 채우기 색상 |
| Stroke | `stroke` | 테두리, 구분선 색상 |

### Color 역할(role) 분류

| 역할 | 용도 | 대표 색상 |
|------|------|-----------|
| `brand` | 브랜드 아이덴티티, 주요 액션 | Blue |
| `accent` | 보조 강조, 딜/프로모션 | Amber |
| `neutral` | 일반 텍스트, 배경, 테두리 | Gray |
| `positive` | 성공, 확정, 완료 | Green |
| `warning` | 경고, 주의 | Yellow |
| `critical` | 에러, 삭제, 위험 | Red |
| `informative` | 안내, 정보성 메시지 | Blue (info) |

### Color 변형(variant) 분류

| 변형 | 용도 |
|------|------|
| *(없음)* | 기본값 (가장 일반적인 사용) |
| `-weak` | 약한/연한 버전 (배경 틴트 등) |
| `-strong` | 강한/진한 버전 |
| `-hover` | 호버 상태 |
| `-pressed` | 눌림 상태 |
| `-disabled` | 비활성 상태 |
| `-on-[surface]` | 특정 표면 위의 텍스트 (예: `fg.on-brand`) |

---

## 토큰 사용 규칙

### DO

```
✅ Semantic Token으로 참조
   background-color: var(--color-bg-brand);

✅ 역할에 맞는 토큰 선택
   에러 메시지 → $color.fg.critical
   성공 배지 → $color.bg.positive
```

### DON'T

```
❌ Raw Value 직접 사용
   background-color: #0077ED;

❌ Scale Token을 컴포넌트에서 직접 참조
   background-color: var(--color-palette-blue-500);

❌ 역할과 맞지 않는 토큰 사용
   에러 메시지에 $color.fg.brand 사용 (의미가 맞지 않음)
```

---

## 테마 확장 (다크 모드)

현재 v1.0은 **라이트 모드**만 정의합니다. 향후 다크 모드 추가 시:

- Level 1 (Raw Value)과 Level 2 (Scale Token)는 변경 없음
- **Level 3 (Semantic Token)의 매핑만 교체**

```
Light Mode:
  $color.bg.neutral     → $color.palette.gray-00  (#FFFFFF)
  $color.fg.neutral     → $color.palette.gray-900 (#1F2430)

Dark Mode:
  $color.bg.neutral     → $color.palette.gray-950 (#111318)
  $color.fg.neutral     → $color.palette.gray-100 (#F0F1F3)
```

이 구조 덕분에 컴포넌트 코드 변경 없이 테마 전환이 가능합니다.

---

## 플랫폼별 토큰 배포 형태

| 플랫폼 | 형태 | 파일 예시 |
|--------|------|-----------|
| Design (Figma) | Variables / Styles | Figma 라이브러리 내 Variables 패널 |
| Web | CSS Custom Properties | `tokens.css` — `--color-bg-brand: #0077ED;` |
| Web (JS) | ES Module 상수 | `tokens.ts` — `export const colorBgBrand = '#0077ED';` |
| iOS | Swift 확장 | `CarmoreTokens.swift` — `static let bgBrand = UIColor(hex: "#0077ED")` |
| Android | XML Resource / Compose | `carmore_colors.xml` — `<color name="carmore_bg_brand">#0077ED</color>` |

> 각 플랫폼의 토큰 변환은 동일한 원본(Foundation 문서)에서 자동 생성하는 것을 목표로 합니다.
