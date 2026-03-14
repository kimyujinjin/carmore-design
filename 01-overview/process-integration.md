# Process Integration

> 디자인 시스템이 기획-디자인-개발 프로세스에 적용되는 방식

---

## 전체 워크플로우

```
┌─────────────────────────────────────────────────────────────────┐
│                        Design System                            │
│                                                                 │
│  Foundation Tokens ──→ Figma Variables ──→ Code Tokens          │
│        │                     │                   │              │
│        ▼                     ▼                   ▼              │
│  Token Docs            Figma Library        CSS Variables       │
│  (color.md,            (Components,         / Swift Constants   │
│   typography.md)        Styles)             / XML Resources     │
│                                                                 │
└─────────────────────────────────────────────────────────────────┘

         │                     │                   │
         ▼                     ▼                   ▼
    ┌─────────┐         ┌───────────┐        ┌──────────┐
    │   PO    │         │ Designer  │        │Developer │
    │ (기획자) │         │ (디자이너) │        │ (개발자)  │
    └─────────┘         └───────────┘        └──────────┘
```

---

## 역할별 활용 방식

### PO (기획자)

**참조 문서:** Overview → Patterns → Components (usage.md)

PO는 디자인 시스템을 **요구사항 명세의 공통 어휘**로 활용합니다.

| 상황 | 활용 예시 |
|------|-----------|
| 새 기능 기획 시 | Patterns 문서를 참고하여 기존 검색 퍼널/예약 플로우와의 일관성 확인 |
| 디자이너에게 전달 시 | "BookingCard(variant=booking)에 취소 버튼을 추가해 주세요" 처럼 컴포넌트명으로 소통 |
| QA 기준 수립 시 | Components usage.md의 Do/Don't를 수용 기준(Acceptance Criteria)에 반영 |

**기획 문서 작성 시 권장 포맷:**

```markdown
## 화면: 검색 결과

- 상단: SearchField(variant="search") — 기존 검색어 유지
- 필터 영역: FilterChip(variant="toggle") 가로 스크롤
- 결과 목록: Card(variant="listing") 리스트
- 결과 없음 시: Empty State 패턴 적용 (04-patterns/empty-states.md)
```

---

### Designer (디자이너)

**참조 문서:** Foundation (전체) → Components (usage.md + style.md) → Collaboration

디자이너는 디자인 시스템을 **Figma 작업의 기반**으로 활용합니다.

#### 디자인 작업 체크리스트

```
□ Figma에서 Carmore Foundation 라이브러리를 연결했는가?
□ 모든 색상은 토큰 변수(Variables)를 사용하고 있는가? (하드코딩 값 금지)
□ 간격은 $dimension.x{N} 단위(4px 배수)를 사용하고 있는가?
□ 텍스트 스타일은 t{N}{Weight} 스케일을 적용하고 있는가?
□ 새로운 패턴이 필요한 경우, 기존 컴포넌트 조합으로 해결 가능한지 검토했는가?
□ 컴포넌트의 모든 상태(States)를 표현했는가? (Default, Hover, Error, Disabled 등)
□ 플랫폼별 차이점을 어노테이션으로 표기했는가?
```

#### 새 컴포넌트 제안 프로세스

```
1. 기존 컴포넌트로 해결 가능한지 확인
   └─ 가능하면 → 기존 컴포넌트 사용 또는 variant 추가 제안
   └─ 불가능하면 → 아래 진행

2. 컴포넌트 제안서 작성
   - 역할과 사용 맥락
   - 기존 컴포넌트와의 차이점
   - 예상 variant 및 state 목록

3. 디자인 시스템 리뷰 (디자이너 + 개발자)

4. 승인 후 _template.md 기반으로 문서화
```

---

### Developer (개발자)

**참조 문서:** Foundation (토큰 값) → Components (style.md) → Platform

개발자는 디자인 시스템을 **구현의 단일 진실 공급원(Single Source of Truth)**으로 활용합니다.

#### 토큰 참조 방식

| 플랫폼 | 토큰 사용 형태 | 예시 |
|--------|---------------|------|
| Web (CSS) | CSS Custom Properties | `var(--color-bg-brand)` |
| Web (JS) | Import 상수 | `import { colorBgBrand } from '@carmore/tokens'` |
| iOS (Swift) | 정적 프로퍼티 | `CarmoreColor.bgBrand` |
| Android (Compose) | Theme 속성 | `CarmoreTheme.colors.bgBrand` |
| Android (XML) | Resource 참조 | `@color/carmore_bg_brand` |

#### 구현 시 체크리스트

```
□ 하드코딩된 색상/간격/폰트 값 대신 토큰을 사용하고 있는가?
□ style.md의 State 매트릭스에 정의된 모든 상태를 구현했는가?
□ 접근성 요구사항(ARIA, 터치 타겟 등)을 반영했는가?
□ 해당 플랫폼 가이드(05-platform/)의 분기 처리를 확인했는가?
□ 컴포넌트 Props가 usage.md의 Options 테이블과 일치하는가?
```

---

## 커뮤니케이션 프로토콜

### 1. 스펙 전달 시 토큰 언어 사용

모든 시각적 속성은 **토큰명으로** 소통합니다.

```
❌ "배경색은 #0077ED로 해주세요"
✅ "$color.bg.brand를 사용해 주세요"

❌ "여백은 16px로 잡아주세요"
✅ "$dimension.x4 간격을 적용해 주세요"

❌ "글씨 크기 14px, 볼드로 해주세요"
✅ "t7Bold를 적용해 주세요"
```

### 2. 컴포넌트 참조 규칙

```
Button(variant="primary", size="lg")
Card(variant="booking")
TextField(variant="search", state="error")
```

### 3. 변경 요청 포맷

디자인 시스템 변경이 필요한 경우:

```markdown
## 변경 요청

- **대상:** Button / style.md
- **유형:** 새 variant 추가
- **내용:** `variant="outline-brand"` — 브랜드 컬러 아웃라인 버튼
- **사용 맥락:** 예약 상세 페이지에서 "예약 변경" 보조 액션
- **영향 범위:** Web, iOS, Android 전 플랫폼
```

---

## 버전 관리

### 디자인 시스템 변경 분류

| 분류 | 설명 | 예시 |
|------|------|------|
| **Patch** (패치) | 토큰 값 미세 조정, 문서 오류 수정 | 색상 밝기 1단계 조정, 오탈자 수정 |
| **Minor** (마이너) | 새 variant 추가, 새 토큰 추가 | Button에 `ghost` variant 추가 |
| **Major** (메이저) | 기존 토큰/컴포넌트 API 변경, 삭제 | 토큰 네이밍 구조 변경 |

### 변경 반영 순서

```
1. 디자인 시스템 문서 업데이트
2. Figma 라이브러리 업데이트 및 퍼블리시
3. 토큰 코드 패키지 업데이트
4. 컴포넌트 코드 업데이트
5. 제품 코드에서 마이그레이션
```

---

## 의사결정 트리: "이건 디자인 시스템에 포함해야 할까?"

```
이 요소가 2개 이상의 화면에서 사용되는가?
├─ No → 해당 화면 전용으로 구현 (시스템 미포함)
└─ Yes
    └─ 기존 컴포넌트의 조합으로 표현 가능한가?
       ├─ Yes → 기존 컴포넌트를 사용하고, 조합 패턴을 Patterns에 문서화
       └─ No
           └─ 기존 컴포넌트에 variant를 추가하면 해결되는가?
              ├─ Yes → variant 추가 후 컴포넌트 문서 업데이트
              └─ No → 새 컴포넌트로 제안 (제안 프로세스 진행)
```
