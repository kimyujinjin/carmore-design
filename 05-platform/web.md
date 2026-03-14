# Web Platform Guide

> 반응형 브레이크포인트, 키보드 내비게이션, CSS 토큰 소비 방식

---

## 1. 반응형 브레이크포인트

| Name | Range | Columns | Page Margin | Gutter |
|------|-------|---------|-------------|--------|
| `sm` (Mobile) | 0 – 599px | 1 | 16px | — |
| `md` (Tablet) | 600 – 1023px | 2 | 24px | 16px |
| `lg` (Desktop) | 1024 – 1439px | 12 (grid) | 32px | 24px |
| `xl` (Wide) | 1440px+ | 12 (grid) | auto (중앙) | 24px |

### 최대 콘텐츠 너비

```css
.container {
  max-width: 1200px;
  margin: 0 auto;
  padding: 0 var(--dimension-spacing-x-page-margin-desktop);
}
```

### 미디어 쿼리 패턴

```css
/* Mobile First */
.component { /* 기본: 모바일 스타일 */ }

@media (min-width: 600px) {
  .component { /* 태블릿 이상 */ }
}

@media (min-width: 1024px) {
  .component { /* 데스크톱 이상 */ }
}

@media (min-width: 1440px) {
  .component { /* 와이드 데스크톱 */ }
}
```

---

## 2. 컴포넌트 반응형 대응

| 컴포넌트 | Mobile (sm) | Tablet (md) | Desktop (lg+) |
|----------|-------------|-------------|----------------|
| **SearchField** | 세로 풀 폭, 개별 단계 | 가로 배치 시작 | 한 줄 가로 배치 |
| **Card (listing)** | 세로 1열 리스트 | 2열 그리드 | 2~3열 그리드 |
| **Card (booking)** | 세로 썸네일 + 텍스트 | 가로 배치 | 가로 배치 (넓게) |
| **BottomSheet** | 하단 슬라이드 | 하단 슬라이드 | **Side Panel로 전환** |
| **Dialog** | 하단 정렬 (width: 100%) | 중앙 정렬 | 중앙 정렬 (max 400px) |
| **FilterChip** | 가로 스크롤 1행 | 가로 스크롤 또는 랩 | 랩 (줄바꿈) |
| **ComparisonTable** | 가로 스크롤 + sticky 열 | 테이블 표시 | 풀 테이블 |
| **Button (CTA)** | width=fill, sticky bottom | width=fill | width=hug, inline |

### BottomSheet → Side Panel 전환

데스크톱(lg 이상)에서 BottomSheet는 **오른쪽 Side Panel**로 전환됩니다.

```
Mobile:                     Desktop:
┌──────────────┐            ┌─────────────────┬──────────┐
│  Content     │            │  Content        │ Side     │
│              │            │                 │ Panel    │
├──────────────┤            │                 │ (필터)   │
│ BottomSheet  │   →        │                 │          │
│ (필터 패널)   │            │                 │          │
└──────────────┘            └─────────────────┴──────────┘
```

| 속성 | Side Panel 값 |
|------|--------------|
| 너비 | 360px (고정) |
| 위치 | 오른쪽 고정 |
| 그림자 | `$elevation.medium` |
| 전환 | `$motion.duration.slow`, `$motion.easing.enter` (좌로 슬라이드) |

---

## 3. 키보드 내비게이션

### 전역 규칙

| 키 | 동작 |
|-----|------|
| `Tab` | 다음 포커스 가능 요소로 이동 |
| `Shift + Tab` | 이전 포커스 가능 요소로 이동 |
| `Enter` / `Space` | 포커스된 요소 활성화 |
| `Escape` | Dialog/BottomSheet/Dropdown 닫기 |
| `Arrow Keys` | 목록/그리드 내 탐색 |

### 포커스 링 스타일

```css
:focus-visible {
  outline: 2px solid var(--color-stroke-brand);
  outline-offset: 2px;
}

/* 마우스 클릭 시에는 포커스 링 숨김 */
:focus:not(:focus-visible) {
  outline: none;
}
```

### 포커스 트랩 (Focus Trap)

Dialog, BottomSheet 등 모달 요소가 열려 있을 때:
- `Tab`/`Shift+Tab`은 모달 내부 요소만 순환
- 배경 요소로 포커스 이동 불가
- `Escape`로 모달 닫기

### Skip Link

```html
<a href="#main-content" class="skip-link">본문으로 건너뛰기</a>
```

---

## 4. CSS 토큰 소비

### CSS Custom Properties

```css
:root {
  /* Color - Palette */
  --color-palette-blue-500: #0077ED;
  --color-palette-amber-400: #FFB314;
  --color-palette-gray-900: #1F2430;

  /* Color - Semantic */
  --color-bg-brand: var(--color-palette-blue-500);
  --color-bg-brand-hover: var(--color-palette-blue-600);
  --color-fg-neutral: var(--color-palette-gray-900);
  --color-fg-on-brand: #FFFFFF;
  --color-stroke-neutral: var(--color-palette-gray-200);

  /* Dimension */
  --dimension-x1: 4px;
  --dimension-x2: 8px;
  --dimension-x4: 16px;
  --dimension-x6: 24px;
  --dimension-x8: 32px;

  /* Radius */
  --radius-sm: 8px;
  --radius-md: 12px;
  --radius-lg: 16px;
  --radius-xl: 20px;
  --radius-full: 9999px;

  /* Typography */
  --font-family-default: 'Pretendard', -apple-system, BlinkMacSystemFont,
    'Segoe UI', system-ui, Roboto, sans-serif;

  /* Motion */
  --motion-duration-fast: 150ms;
  --motion-duration-normal: 250ms;
  --motion-duration-slow: 350ms;
  --motion-easing-standard: cubic-bezier(0.4, 0.0, 0.2, 1.0);
}
```

### 네이밍 변환 규칙

디자인 토큰 → CSS Custom Property:

| 디자인 토큰 | CSS 변수 |
|------------|----------|
| `$color.bg.brand` | `--color-bg-brand` |
| `$color.fg.neutral-weak` | `--color-fg-neutral-weak` |
| `$dimension.x4` | `--dimension-x4` |
| `$radius.md` | `--radius-md` |
| `$motion.duration.fast` | `--motion-duration-fast` |

변환 규칙: `.` → `-`, `$` 제거, `--` 접두사 추가

---

## 5. 폰트 로딩

### Pretendard

```html
<link rel="preconnect" href="https://cdn.jsdelivr.net" />
<link
  rel="stylesheet"
  href="https://cdn.jsdelivr.net/gh/orioncactus/pretendard/dist/web/variable/pretendardvariable.min.css"
/>
```

### 폰트 로딩 전략

```css
@font-face {
  font-family: 'Pretendard';
  font-display: swap; /* FOUT 허용, CLS 방지 */
}
```

- `font-display: swap`으로 폰트 로딩 전 시스템 폰트 표시
- 핵심 weight(400, 500, 700)만 preload

---

## 6. 접근성 (Web 고유)

| 항목 | 구현 |
|------|------|
| Color scheme | `<meta name="color-scheme" content="light">` |
| Reduced motion | `@media (prefers-reduced-motion: reduce)` 대응 |
| High contrast | `@media (prefers-contrast: more)` — 테두리 강화 |
| 화면 확대 | 200% 확대 시에도 콘텐츠 잘림 없음 |
| 텍스트 크기 | `rem` 단위 사용으로 브라우저 기본 글꼴 크기 존중 |
| 링크 구분 | 색상 + 밑줄로 이중 표시 |

---

## 7. 성능 고려사항

| 항목 | 가이드라인 |
|------|-----------|
| 이미지 | `loading="lazy"`, WebP/AVIF 우선, `srcset` 반응형 |
| CLS 방지 | 이미지/카드에 `aspect-ratio` 지정, 스켈레톤 레이아웃 매칭 |
| 인터랙션 | 호버/포커스 전환은 `will-change: transform` 최소화 |
| 토큰 CSS | 사용하는 토큰만 포함 (tree-shaking) |
