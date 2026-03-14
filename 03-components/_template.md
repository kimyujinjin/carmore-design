# Component Template

> 새로운 컴포넌트를 문서화할 때 이 템플릿을 복사하여 사용합니다.

---

## usage.md 구조

```markdown
# [Component Name]

> 한 줄 역할 설명

---

## 1. 설명 (Description)

컴포넌트의 역할, 언제 사용하는지, 어떤 문제를 해결하는지 간략히 서술합니다.

---

## 2. 해부도 (Anatomy)

컴포넌트를 구성하는 파트(part)를 번호로 표시합니다.

```
┌──────────────────────────┐
│ ① [Part 1] ② [Part 2]   │ ③ Container
└──────────────────────────┘
```

| # | Part | 필수 여부 | 설명 |
|---|------|-----------|------|
| ① | Part 1 | 필수 | ... |
| ② | Part 2 | 선택 | ... |
| ③ | Container | 필수 | ... |

---

## 3. 옵션 (Options / Props)

| Property | Type | Values | Default | 설명 |
|----------|------|--------|---------|------|
| variant | enum | "primary" \| "secondary" | "primary" | 시각적 변형 |
| size | enum | "sm" \| "md" \| "lg" | "md" | 크기 |
| disabled | boolean | true \| false | false | 비활성 상태 |

---

## 4. 인터랙션 (Interactions)

| 입력 | 동작 |
|------|------|
| Click / Tap | ... |
| Hover (Web) | ... |
| Focus (Keyboard) | ... |
| Long Press | ... |

---

## 5. 가이드라인 (Do & Don't)

### DO
- ✅ [올바른 사용 예시]

### DON'T
- ❌ [잘못된 사용 예시]

---

## 6. 플랫폼 차이 (Platform Differences)

| 항목 | Web | iOS | Android |
|------|-----|-----|---------|
| [차이점 1] | ... | ... | ... |

---

## 7. 접근성 (Accessibility)

| 속성 | 값 |
|------|-----|
| Role | ... |
| ARIA / 접근성 속성 | ... |
| 키보드 | ... |
| 스크린 리더 | ... |
```

---

## style.md 구조

```markdown
# [Component Name] — Style Spec

> 토큰 매핑, 상태별 스펙, 레이아웃 치수

---

## 1. Anatomy 참조

| Part | Token Slot |
|------|-----------|
| Container | background, border, radius, elevation |
| Label | color, typography |
| Icon | color, size |

---

## 2. Variants

| Variant | 설명 |
|---------|------|
| primary | ... |
| secondary | ... |

---

## 3. States

| State | 조건 | 시각적 변화 |
|-------|------|------------|
| enabled | 기본 | — |
| hovered | 마우스 오버 (Web) | 배경색 변경 |
| pressed | 클릭/탭 중 | 배경색 변경 |
| focused | 키보드 포커스 | 포커스 링 |
| disabled | disabled=true | 투명도 감소, 인터랙션 불가 |

---

## 4. Layout Spec

| Size | Height | Padding X | Padding Y | Min Width |
|------|--------|-----------|-----------|-----------|
| sm | ... | ... | ... | ... |
| md | ... | ... | ... | ... |
| lg | ... | ... | ... | ... |

---

## 5. Color Spec

### variant="primary"

| State | Container BG | Container Stroke | Label Color | Icon Color |
|-------|-------------|------------------|-------------|------------|
| enabled | token | token | token | token |
| hovered | token | token | token | token |
| pressed | token | token | token | token |
| disabled | token | token | token | token |

---

## 6. Typography Spec

| Size | Token |
|------|-------|
| sm | ... |
| md | ... |
| lg | ... |

---

## 7. Motion Spec

| Transition | Duration | Easing |
|-----------|----------|--------|
| 색상 전환 | ... | ... |
| 등장/퇴장 | ... | ... |
```
