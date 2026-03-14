# Handoff Guide

> 디자이너에서 개발자로의 디자인 스펙 전달 프로세스

---

## 1. 개요

핸드오프는 디자이너의 Figma 작업물을 개발자가 **정확하게 구현**할 수 있도록 스펙을 전달하는 과정입니다. Carmore Design System의 토큰 체계를 활용하면 "이 색상이 뭐예요?", "여백이 몇 px이에요?" 같은 질문을 최소화할 수 있습니다.

---

## 2. Figma Dev Mode 활용

### 디자이너가 준비할 것

```
□ 모든 색상이 Variable(토큰)로 적용되어 있는가?
□ 간격/패딩이 Variable로 적용되어 있는가?
□ 텍스트에 Text Style이 적용되어 있는가?
□ 컴포넌트가 라이브러리 인스턴스인가? (Detach 없음)
□ 각 화면의 상태(State)가 별도 프레임으로 표현되어 있는가?
□ 플랫폼별 차이점이 어노테이션으로 표기되어 있는가?
□ Ready for dev 상태로 마킹했는가?
```

### 개발자가 확인할 것

```
□ Dev Mode에서 컴포넌트명과 variant 확인
□ Properties 패널에서 적용된 Variable(토큰) 확인
□ CSS/iOS/Android 탭에서 플랫폼별 값 확인
□ Inspect 패널에서 간격/정렬 확인
□ 해당 컴포넌트의 style.md에서 토큰 매핑 교차 확인
```

---

## 3. 토큰 참조 형식

핸드오프 시 모든 시각적 속성은 **토큰명으로 명시**합니다.

### 어노테이션 형식

```
🎨 Color
  배경: $color.bg.brand
  텍스트: $color.fg.on-brand
  테두리: $color.stroke.neutral

📏 Layout
  패딩: $dimension.spacing.card-padding (16px)
  아이템 간격: $dimension.spacing-y.component-gap (8px)
  페이지 마진: $dimension.spacing-x.page-margin (16px)

🔤 Typography
  제목: $typography.title3
  본문: $typography.body1
  가격: $typography.price

📐 Shape
  모서리: $radius.md (12px)
  그림자: $elevation.low

🎬 Motion
  호버 전환: $motion.duration.fast, $motion.easing.standard
```

### 스펙 시트 예시 (카드 컴포넌트)

```
┌──────────────────────────────────────────────────┐
│  Component: Card (variant="listing", vertical)   │
├──────────────────────────────────────────────────┤
│  Container                                       │
│  ├─ bg: $color.bg.neutral                        │
│  ├─ stroke: $color.stroke.neutral (1px)          │
│  ├─ radius: $radius.md (12px)                    │
│  ├─ elevation: $elevation.low                    │
│  └─ padding: 0 (이미지 full-bleed) / 16px (텍스트)│
│                                                  │
│  Image                                           │
│  ├─ ratio: 16:9                                  │
│  ├─ radius: $radius.sm (8px) (top만)             │
│  └─ placeholder: $color.bg.neutral-weak          │
│                                                  │
│  Title: "현대 아반떼 2026"                         │
│  ├─ typography: $typography.title3                │
│  └─ color: $color.fg.neutral                     │
│                                                  │
│  Location: "📍 서울 강남"                          │
│  ├─ typography: $typography.body2                 │
│  └─ color: $color.fg.neutral-weak                │
│                                                  │
│  Price: "₩45,000/일"                             │
│  ├─ typography: $typography.price                 │
│  └─ color: $color.fg.neutral                     │
│                                                  │
│  Spacing                                         │
│  ├─ image → title: $dimension.x3 (12px)          │
│  ├─ title → location: $dimension.x1 (4px)        │
│  └─ location → price: $dimension.x2 (8px)        │
└──────────────────────────────────────────────────┘
```

---

## 4. 상태 문서화 체크리스트

디자이너는 각 화면/컴포넌트에 대해 아래 상태를 Figma에서 표현해야 합니다.

### 화면 레벨

| 상태 | 설명 | 필수 |
|------|------|------|
| Default | 정상 상태 (데이터 있음) | ✅ |
| Loading | 데이터 로딩 중 (스켈레톤) | ✅ |
| Empty | 데이터 없음 | ✅ |
| Error | 에러 발생 | ✅ |
| Partial | 일부 데이터만 로드됨 | 선택 |

### 컴포넌트 레벨

| 상태 | 해당 컴포넌트 | 필수 |
|------|-------------|------|
| Enabled | 전체 | ✅ |
| Hovered | Button, Card, TextField | ✅ (Web) |
| Pressed | Button, Card, FilterChip | ✅ |
| Focused | TextField, Button | ✅ |
| Disabled | 전체 | ✅ |
| Error | TextField | ✅ |
| Loading | Button | ✅ |
| Selected | FilterChip, Card | 해당 시 |

---

## 5. 플랫폼 어노테이션

플랫폼별로 다르게 구현되어야 하는 부분은 Figma에서 어노테이션으로 표기합니다.

### 어노테이션 형식

```
📱 Platform Note
━━━━━━━━━━━━━━━
iOS: UISheetPresentationController (medium detent)
Android: ModalBottomSheet (halfExpanded)
Web: 데스크톱에서 Side Panel로 전환 (lg 브레이크포인트)
```

### 색상 코드

| 어노테이션 색상 | 의미 |
|---------------|------|
| 🔵 파란색 | 일반 스펙 설명 |
| 🟡 노란색 | 플랫폼별 차이점 |
| 🔴 빨간색 | 주의/예외 사항 |
| 🟢 초록색 | 인터랙션/모션 설명 |

---

## 6. 핸드오프 미팅 가이드

### 미팅 전 (디자이너)

```
□ 모든 화면 상태 (Default, Loading, Empty, Error) 표현 완료
□ 컴포넌트 상태 (Enabled, Hover, Pressed, Disabled 등) 표현 완료
□ 토큰 어노테이션 작성 완료
□ 플랫폼 차이점 어노테이션 작성 완료
□ Figma 프로토타입 연결 (인터랙션 플로우 확인용)
□ Ready for dev 마킹 완료
```

### 미팅 중 (공동)

```
1. 전체 플로우 워크스루 (프로토타입 기반)
2. 화면별 상태 및 분기 확인
3. 컴포넌트 variant/state 확인
4. 플랫폼별 차이점 합의
5. 엣지 케이스 논의 (긴 텍스트, 다국어, 큰 데이터 등)
6. 질문 및 미결 사항 정리
```

### 미팅 후 (개발자)

```
□ 미결 사항 → Figma 코멘트로 질문 (디자이너 태그)
□ 구현 중 토큰 불일치 발견 시 → 디자이너에게 확인
□ 새 상태/엣지 케이스 발견 시 → 디자이너에게 보완 요청
```

---

## 7. 자주 묻는 질문

### "Figma에 없는 상태는 어떻게 구현하나요?"

→ style.md의 State 매트릭스를 참조합니다. Figma에 모든 상태가 그려져 있지 않더라도, 토큰 기반으로 올바른 상태를 구현할 수 있습니다.

### "토큰이 아닌 하드코딩된 값을 발견했어요"

→ 디자이너에게 알려서 토큰으로 교체하도록 합니다. 개발자는 가장 근사한 토큰을 적용하고 디자이너에게 확인합니다.

### "디자인과 구현 결과가 1~2px 다릅니다"

→ 토큰 값이 동일하면 허용 범위입니다. 플랫폼별 렌더링 차이(서브픽셀, 안티앨리어싱)는 발생할 수 있습니다. 토큰 값 자체가 다르면 수정합니다.
