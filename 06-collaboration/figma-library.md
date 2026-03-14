# Figma Library

> Figma 라이브러리 구조화, 토큰 변수, 컴포넌트 배포 전략

---

## 1. 라이브러리 구조

Carmore Figma 라이브러리는 **2개의 독립 라이브러리**로 분리합니다.

```
📁 Carmore Design System
├── 📦 Carmore Foundation        ← 토큰 + 스타일 라이브러리
│   ├── Variables (Color, Spacing, Radius)
│   ├── Text Styles (Typography)
│   ├── Effect Styles (Elevation)
│   └── Color Styles (legacy 호환용)
│
└── 📦 Carmore Components       ← UI 컴포넌트 라이브러리
    ├── Button
    ├── TextField
    ├── Card (base / booking / listing)
    ├── BottomSheet
    ├── Dialog
    ├── FilterChip
    └── ComparisonTable
```

### 분리 이유

| 이유 | 설명 |
|------|------|
| **독립 업데이트** | 토큰 값 변경 시 Foundation만 퍼블리시 → Component 자동 반영 |
| **파일 크기** | Foundation은 가볍고, Components는 무거움 → 분리로 성능 유지 |
| **권한 분리** | Foundation은 디자인 시스템 팀만 편집, Components는 기여 가능 |

---

## 2. Figma Variables 구성

### Collection 구조

```
📁 Variables
├── 📂 Color
│   ├── 📋 Palette         ← Scale tokens (blue-500, gray-200 등)
│   └── 📋 Semantic        ← Semantic tokens (bg/brand, fg/neutral 등)
│
├── 📂 Dimension
│   ├── 📋 Scale           ← x1, x2, x4 등 기본 스케일
│   └── 📋 Spacing         ← 시맨틱 간격 (card-padding, page-margin 등)
│
└── 📂 Radius
    └── 📋 Scale           ← none, sm, md, lg, xl, full
```

### Variable 네이밍

Figma Variables에서는 `/`로 계층을 구분합니다.

| 디자인 토큰 | Figma Variable Name |
|------------|---------------------|
| `$color.palette.blue-500` | `color/palette/blue-500` |
| `$color.bg.brand` | `color/semantic/bg/brand` |
| `$color.fg.neutral-weak` | `color/semantic/fg/neutral-weak` |
| `$dimension.x4` | `dimension/scale/x4` |
| `$dimension.spacing.card-padding` | `dimension/spacing/card-padding` |
| `$radius.md` | `radius/md` |

### Mode (테마) 설정

| Collection | Mode 1 | Mode 2 (향후) |
|-----------|--------|--------------|
| Color/Semantic | Light | Dark |
| Dimension | Default | Compact (향후) |

> v1.0에서는 Light 모드만 구현합니다. Variable 구조는 Dark 모드 확장에 대비합니다.

---

## 3. 컴포넌트 페이지 구조

### Carmore Components 파일 내 페이지

```
📄 Cover                     ← 라이브러리 표지
📄 —— Atoms ——               ← 구분선
📄 Button                    ← 모든 variant × size × state
📄 TextField                 ← default + search variant
📄 FilterChip                ← toggle + selection + removable
📄 —— Molecules ——           ← 구분선
📄 Card                      ← base + booking + listing
📄 ComparisonTable            ← side-by-side + stacked
📄 —— Overlays ——            ← 구분선
📄 BottomSheet               ← modal + persistent
📄 Dialog                    ← alert + confirm + destructive
📄 —— Patterns ——            ← 구분선
📄 Search Bar                ← 조합 패턴 (TextField + Button)
📄 Filter Bar                ← 조합 패턴 (FilterChip 그룹)
📄 —— Documentation ——       ← 구분선
📄 Changelog                 ← 버전별 변경 이력
```

---

## 4. 컴포넌트 설계 규칙

### Variant Property 네이밍

```
컴포넌트 이름: carmore/[category]/[name]

예시:
carmore/button/primary
carmore/card/listing
carmore/dialog/confirm
```

### Component Properties

| Property Type | 용도 | 예시 |
|--------------|------|------|
| **Variant** | 시각적 변형 | `variant`: primary / secondary / tertiary |
| **Enum** | 고정 옵션 | `size`: sm / md / lg |
| **Boolean** | on/off 토글 | `showIcon`: true / false |
| **Text** | 동적 텍스트 | `label`: "예약하기" |
| **Instance Swap** | 아이콘 교체 | `icon`: ic_action_search |

### Auto Layout 규칙

- 모든 컴포넌트는 Auto Layout 기반
- padding/gap 값은 **반드시 Variable 참조** (하드코딩 금지)
- Resizing: `Hug contents` (기본) 또는 `Fill container`

### 상태(State) 표현

| 방식 | 용도 |
|------|------|
| **Variant property** | `state`: enabled / hovered / pressed / disabled |
| **Interactive Component** | Prototype에서 hover/press 전환 (프리뷰용) |

---

## 5. 퍼블리시 워크플로우

### 브랜치 전략

```
main (프로덕션)
├── feature/button-ghost-variant    ← 새 variant 추가
├── fix/card-padding                ← 토큰 수정
└── update/color-palette            ← 팔레트 변경
```

### 퍼블리시 체크리스트

```
□ 변경 사항이 디자인 시스템 문서와 일치하는가?
□ 모든 variant × state 조합이 올바른가?
□ Variable 참조가 깨진 곳이 없는가? (Detached styles 없음)
□ Auto Layout이 정상 작동하는가? (리사이즈 테스트)
□ 변경 이력을 Changelog 페이지에 기록했는가?
□ 리뷰어의 승인을 받았는가?
```

### 퍼블리시 순서

```
1. Foundation 라이브러리 퍼블리시 (토큰 변경 시)
2. Components 라이브러리 업데이트 → Foundation 변경 수용
3. Components 라이브러리 퍼블리시
4. 제품 파일에서 "Updates available" 수용
```

---

## 6. 사용자 가이드

### 디자이너가 새 화면을 만들 때

```
1. 새 Figma 파일 생성
2. Assets 패널 → Carmore Foundation + Components 라이브러리 활성화
3. 프레임 생성 (Mobile: 390px, Tablet: 768px, Desktop: 1440px)
4. Variables 패널에서 Color/Dimension 토큰 적용
5. Components 라이브러리에서 컴포넌트 인스턴스 삽입
6. 하드코딩된 값 없이 모든 속성을 토큰/스타일로 적용
```

### Figma 프레임 크기 프리셋

| 디바이스 | Width | 비고 |
|---------|-------|------|
| iPhone 15 | 393px | iOS 기본 |
| iPhone 15 Pro Max | 430px | iOS 대형 |
| Android (기본) | 360px | Android 기본 |
| Android (대형) | 412px | Pixel 시리즈 |
| Tablet | 768px | iPad Mini 세로 |
| Desktop | 1440px | 표준 데스크톱 |
