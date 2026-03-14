# Carmore Design System

> 글로벌 렌터카 및 숙박 예약 플랫폼을 위한 통합 디자인 시스템

Carmore Design System은 Web, iOS, Android 전 플랫폼에서 일관된 사용자 경험을 제공하기 위한 디자인 언어, 토큰, 컴포넌트, 패턴의 집합입니다. 기획자(PO), 디자이너, 개발자 간의 커뮤니케이션 비용을 최소화하고, 제품 품질을 체계적으로 관리하는 것을 목표로 합니다.

---

## 목차

### 1. Overview

| 문서 | 설명 |
|------|------|
| [Vision & Principles](./01-overview/vision-and-principles.md) | 디자인 철학과 핵심 원칙 |
| [Process Integration](./01-overview/process-integration.md) | 기획-디자인-개발 협업 프로세스 |

### 2. Foundation

| 문서 | 설명 |
|------|------|
| [Design Tokens](./02-foundation/design-tokens.md) | 3단계 토큰 아키텍처 개요 |
| [Color](./02-foundation/color.md) | 팔레트, 스케일, 시맨틱 컬러 토큰 |
| [Typography](./02-foundation/typography.md) | 타입 스케일 및 플랫폼별 폰트 |
| [Spacing & Radius](./02-foundation/spacing-and-radius.md) | 4pt 그리드 간격 및 모서리 곡률 |
| [Elevation](./02-foundation/elevation.md) | 그림자 및 깊이 시스템 |
| [Iconography](./02-foundation/iconography.md) | 아이콘 제작 기준 및 네이밍 |
| [Motion](./02-foundation/motion.md) | 애니메이션 토큰 |

### 3. Components

| 컴포넌트 | Usage | Style | 설명 |
|----------|-------|-------|------|
| [Button](./03-components/button/) | [usage](./03-components/button/usage.md) | [style](./03-components/button/style.md) | 주요 액션 트리거 |
| [TextField](./03-components/text-field/) | [usage](./03-components/text-field/usage.md) | [style](./03-components/text-field/style.md) | 텍스트 입력 (검색 포함) |
| [Card](./03-components/card/) | [usage](./03-components/card/usage.md) | [style](./03-components/card/style.md) | 콘텐츠 컨테이너 (예약/리스팅) |
| [BottomSheet](./03-components/bottom-sheet/) | [usage](./03-components/bottom-sheet/usage.md) | [style](./03-components/bottom-sheet/style.md) | 하단 패널 |
| [Dialog](./03-components/dialog/) | [usage](./03-components/dialog/usage.md) | [style](./03-components/dialog/style.md) | 확인/알림 대화상자 |
| [FilterChip](./03-components/filter-chip/) | [usage](./03-components/filter-chip/usage.md) | [style](./03-components/filter-chip/style.md) | 필터 토글 칩 |
| [ComparisonTable](./03-components/comparison-table/) | [usage](./03-components/comparison-table/usage.md) | [style](./03-components/comparison-table/style.md) | 상품 비교 테이블 |

### 4. Patterns

| 문서 | 설명 |
|------|------|
| [Search Funnel](./04-patterns/search-funnel.md) | 검색 퍼널 플로우 |
| [Booking Flow](./04-patterns/booking-flow.md) | 예약 플로우 |
| [Form Input](./04-patterns/form-input.md) | 폼 입력 패턴 |
| [Empty States](./04-patterns/empty-states.md) | 빈 화면 패턴 |
| [Loading States](./04-patterns/loading-states.md) | 로딩 상태 패턴 |

### 5. Platform

| 문서 | 설명 |
|------|------|
| [Web](./05-platform/web.md) | 반응형 및 웹 가이드라인 |
| [iOS](./05-platform/ios.md) | iOS 네이티브 대응 |
| [Android](./05-platform/android.md) | Android 네이티브 대응 |

### 6. Collaboration

| 문서 | 설명 |
|------|------|
| [Figma Library](./06-collaboration/figma-library.md) | Figma 라이브러리 구조화 |
| [Handoff Guide](./06-collaboration/handoff-guide.md) | 디자인-개발 핸드오프 |
| [Migration Strategy](./06-collaboration/migration-strategy.md) | 레거시 마이그레이션 전략 |

---

## 빠른 참조

### 토큰 네이밍 규칙

```
컬러:    $color.[property].[role]-[variant]     예) $color.bg.brand, $color.fg.neutral-weak
간격:    $dimension.x{N}                        예) $dimension.x4 = 16px
타이포:  t{N}{Weight}                           예) t5Medium = 16px/Medium
곡률:    $radius.{size}                         예) $radius.md = 12px
그림자:  $elevation.{level}                     예) $elevation.low
모션:    $motion.duration.{speed}               예) $motion.duration.fast = 150ms
```

### 플랫폼별 기본 폰트

| 플랫폼 | 폰트 |
|--------|------|
| Web | Pretendard, system-ui, sans-serif |
| iOS | SF Pro (시스템 기본) |
| Android | Pretendard (번들) / Roboto (폴백) |

---

## 버전

| 버전 | 날짜 | 변경 내용 |
|------|------|-----------|
| 1.0.0 | 2026-03-12 | 디자인 시스템 초안 작성 |
