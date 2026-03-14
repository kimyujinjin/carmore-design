# Elevation

> 그림자(Shadow)를 활용한 깊이 시스템

---

## 개요

Elevation은 UI 요소 간의 **시각적 깊이와 계층**을 표현합니다. 그림자의 크기와 진하기로 요소가 표면에서 얼마나 떠 있는지를 나타내며, 사용자가 인터랙션 가능한 요소와 콘텐츠 층을 직관적으로 구분할 수 있게 합니다.

---

## Elevation Scale

| Token | Box Shadow | 용도 |
|-------|-----------|------|
| `$elevation.none` | `none` | 평면 요소, 인라인 콘텐츠 |
| `$elevation.low` | `0 1px 3px rgba(0,0,0,0.08), 0 1px 2px rgba(0,0,0,0.06)` | 카드, 리스트 아이템 |
| `$elevation.medium` | `0 4px 12px rgba(0,0,0,0.10), 0 2px 4px rgba(0,0,0,0.06)` | 드롭다운, 팝오버, 툴팁 |
| `$elevation.high` | `0 12px 32px rgba(0,0,0,0.14), 0 4px 8px rgba(0,0,0,0.08)` | BottomSheet, Dialog, 모달 |

---

## 컴포넌트별 Elevation 매핑

| 컴포넌트 | Token | 비고 |
|----------|-------|------|
| Card (기본) | `$elevation.low` | 기본 카드 그림자 |
| Card (호버) | `$elevation.medium` | 호버 시 그림자 강화 |
| FilterChip | `$elevation.none` | 칩은 평면 |
| Dropdown / Popover | `$elevation.medium` | 떠 있는 메뉴 |
| BottomSheet | `$elevation.high` | 화면 위로 슬라이드 |
| Dialog | `$elevation.high` | 오버레이 위 |
| Tooltip | `$elevation.medium` | 콘텐츠 위 |
| Navigation Bar (고정) | `$elevation.low` | 스크롤 시 구분 |

---

## 플랫폼 매핑

### Web (CSS)

```css
:root {
  --elevation-none: none;
  --elevation-low: 0 1px 3px rgba(0,0,0,0.08), 0 1px 2px rgba(0,0,0,0.06);
  --elevation-medium: 0 4px 12px rgba(0,0,0,0.10), 0 2px 4px rgba(0,0,0,0.06);
  --elevation-high: 0 12px 32px rgba(0,0,0,0.14), 0 4px 8px rgba(0,0,0,0.08);
}
```

### iOS

| Token | iOS 구현 |
|-------|---------|
| `$elevation.low` | `shadowRadius: 3, shadowOffset: (0, 1), shadowOpacity: 0.08` |
| `$elevation.medium` | `shadowRadius: 12, shadowOffset: (0, 4), shadowOpacity: 0.10` |
| `$elevation.high` | `shadowRadius: 32, shadowOffset: (0, 12), shadowOpacity: 0.14` |

### Android

| Token | Material Elevation |
|-------|-------------------|
| `$elevation.low` | 2dp |
| `$elevation.medium` | 8dp |
| `$elevation.high` | 16dp |

---

## 사용 가이드라인

### DO

- 콘텐츠 계층에 따라 일관되게 적용합니다 (페이지 < 카드 < 팝오버 < 모달)
- 호버/눌림 시 elevation 변화로 인터랙션 피드백을 제공합니다

### DON'T

- 같은 계층의 요소에 서로 다른 elevation을 적용하지 않습니다
- 과도한 그림자로 시각적 노이즈를 만들지 않습니다
- `$elevation.high`를 일반 카드에 사용하지 않습니다 (모달/시트 전용)
