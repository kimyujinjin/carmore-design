# Typography

> 타입 스케일, 플랫폼별 폰트 패밀리, 시맨틱 타이포그래피 토큰

---

## 개요

Carmore의 타이포그래피 시스템은 **10단계 크기 스케일**과 **3단계 굵기**를 조합하여 구성됩니다. 렌터카/숙박 예약 서비스 특성상 가격, 날짜, 위치 등 밀도 높은 정보를 명확하게 전달하는 것이 핵심입니다.

---

## 1. 플랫폼별 폰트 패밀리

| 플랫폼 | Primary Font | Fallback |
|--------|-------------|----------|
| **Web** | Pretendard | -apple-system, BlinkMacSystemFont, "Segoe UI", system-ui, Roboto, sans-serif |
| **iOS** | SF Pro (시스템 기본) | — |
| **Android** | Pretendard (앱 번들) | Roboto |

### 선택 근거

- **Pretendard**: CJK(한/중/일) + Latin 모두 우수한 가독성. 글로벌 서비스에 적합한 다국어 지원
- **SF Pro (iOS)**: Apple 네이티브 시스템 폰트 사용으로 iOS 사용자에게 익숙한 읽기 경험 제공
- **Roboto (Android 폴백)**: Pretendard가 로드되지 않을 경우의 안전망

### Web 폰트 스택 CSS

```css
:root {
  --font-family-default: 'Pretendard', -apple-system, BlinkMacSystemFont,
    'Segoe UI', system-ui, Roboto, 'Helvetica Neue', sans-serif;
}
```

---

## 2. Type Scale (타입 스케일)

토큰 형식: `t{N}{Weight}` — N은 크기 단계(1=가장 큼, 10=가장 작음), Weight는 굵기

### 스케일 테이블

| 단계 | Size (px) | Size (rem) | Line Height (px) | Line Height (rem) | Letter Spacing |
|------|-----------|------------|-------------------|--------------------|----------------|
| **t1** | 28 | 1.75 | 36 | 2.25 | -0.02em |
| **t2** | 24 | 1.5 | 32 | 2.0 | -0.01em |
| **t3** | 20 | 1.25 | 28 | 1.75 | -0.01em |
| **t4** | 18 | 1.125 | 26 | 1.625 | -0.005em |
| **t5** | 16 | 1.0 | 24 | 1.5 | 0 |
| **t6** | 15 | 0.9375 | 22 | 1.375 | 0 |
| **t7** | 14 | 0.875 | 20 | 1.25 | 0 |
| **t8** | 13 | 0.8125 | 18 | 1.125 | 0.005em |
| **t9** | 12 | 0.75 | 16 | 1.0 | 0.01em |
| **t10** | 11 | 0.6875 | 14 | 0.875 | 0.015em |

### Weight (굵기)

| Weight | 값 | 사용 |
|--------|-----|------|
| **Regular** | 400 | 본문, 설명문, 보조 텍스트 |
| **Medium** | 500 | 강조 본문, 라벨, 부제목 |
| **Bold** | 700 | 제목, CTA, 가격 |

### 조합 예시

| 토큰 | Size | Weight | 전형적 용도 |
|------|------|--------|------------|
| `t1Bold` | 28px | Bold | 페이지 타이틀 ("서울 렌터카") |
| `t2Bold` | 24px | Bold | 섹션 제목 ("인기 차량") |
| `t3Bold` | 20px | Bold | 카드 타이틀, 서브헤딩 |
| `t3Medium` | 20px | Medium | 대형 부제목 |
| `t4Medium` | 18px | Medium | 강조 본문, 소제목 |
| `t5Regular` | 16px | Regular | **기본 본문** (Default body) |
| `t5Medium` | 16px | Medium | 강조 본문 |
| `t5Bold` | 16px | Bold | 가격 표시 ("₩45,000/일") |
| `t6Regular` | 15px | Regular | 밀도 높은 본문 |
| `t7Regular` | 14px | Regular | 보조 본문, 메타데이터 |
| `t7Medium` | 14px | Medium | 라벨, 필터 칩 텍스트 |
| `t7Bold` | 14px | Bold | 버튼 라벨 (sm) |
| `t8Regular` | 13px | Regular | 캡션 |
| `t8Medium` | 13px | Medium | 강조 캡션 |
| `t9Regular` | 12px | Regular | 작은 캡션, 배지 텍스트 |
| `t9Medium` | 12px | Medium | 강조 배지, 태그 |
| `t10Regular` | 11px | Regular | 법적 고지, 최소 텍스트 |

---

## 3. Semantic Typography Token (시맨틱 타이포그래피 토큰)

역할 기반으로 스케일 토큰을 매핑한 의미론적 토큰입니다. 컴포넌트에서는 이 토큰을 사용합니다.

| Semantic Token | Scale Token 참조 | Size | Weight | 용도 |
|----------------|------------------|------|--------|------|
| `$typography.display1` | `t1Bold` | 28px | Bold | 히어로 타이틀 |
| `$typography.title1` | `t1Bold` | 28px | Bold | 페이지 타이틀 |
| `$typography.title2` | `t2Bold` | 24px | Bold | 섹션 제목 |
| `$typography.title3` | `t3Bold` | 20px | Bold | 카드/다이얼로그 타이틀 |
| `$typography.subtitle1` | `t4Medium` | 18px | Medium | 대형 부제목 |
| `$typography.subtitle2` | `t5Medium` | 16px | Medium | 소형 부제목 |
| `$typography.body1` | `t5Regular` | 16px | Regular | 기본 본문 |
| `$typography.body1-emphasis` | `t5Medium` | 16px | Medium | 강조 본문 |
| `$typography.body2` | `t7Regular` | 14px | Regular | 보조 본문 |
| `$typography.body2-emphasis` | `t7Medium` | 14px | Medium | 강조 보조 본문 |
| `$typography.caption1` | `t8Regular` | 13px | Regular | 캡션 |
| `$typography.caption2` | `t9Regular` | 12px | Regular | 소형 캡션 |
| `$typography.label1` | `t5Bold` | 16px | Bold | 버튼 라벨 (lg/md) |
| `$typography.label2` | `t7Bold` | 14px | Bold | 버튼 라벨 (sm), 강조 라벨 |
| `$typography.label3` | `t9Medium` | 12px | Medium | 칩, 배지 라벨 |
| `$typography.price` | `t5Bold` | 16px | Bold | 가격 표시 |
| `$typography.price-large` | `t3Bold` | 20px | Bold | 대형 가격 표시 |

---

## 4. 플랫폼별 매핑

### iOS

iOS에서는 SF Pro 시스템 폰트의 Dynamic Type을 지원합니다.

| Semantic Token | iOS Text Style | Size (기본) |
|----------------|---------------|-------------|
| `$typography.title1` | `.title1` | 28pt |
| `$typography.title2` | `.title2` | 22pt |
| `$typography.title3` | `.title3` | 20pt |
| `$typography.subtitle1` | `.headline` | 17pt |
| `$typography.body1` | `.body` | 17pt |
| `$typography.body2` | `.subheadline` | 15pt |
| `$typography.caption1` | `.caption1` | 12pt |
| `$typography.caption2` | `.caption2` | 11pt |
| `$typography.label1` | `.body` (Bold) | 17pt |

> iOS에서는 접근성 > 큰 텍스트 설정을 존중하여 Dynamic Type이 적용됩니다.

### Android

| Semantic Token | Material 3 Style | Size (기본) |
|----------------|------------------|-------------|
| `$typography.title1` | `headlineLarge` | 28sp |
| `$typography.title2` | `headlineMedium` | 24sp |
| `$typography.title3` | `titleLarge` | 20sp |
| `$typography.subtitle1` | `titleMedium` | 18sp |
| `$typography.body1` | `bodyLarge` | 16sp |
| `$typography.body2` | `bodyMedium` | 14sp |
| `$typography.caption1` | `bodySmall` | 13sp |
| `$typography.caption2` | `labelSmall` | 12sp |
| `$typography.label1` | `labelLarge` | 16sp |

> Android에서는 sp 단위를 사용하여 사용자의 글꼴 크기 설정을 존중합니다.

---

## 5. 사용 가이드라인

### DO

- **정보 위계를 3단계 이내로 유지합니다**
  ```
  Title (t3Bold) → Body (t5Regular) → Caption (t8Regular)
  ```

- **가격은 항상 Bold로 표시합니다**
  ```
  ₩45,000/일  →  $typography.price (t5Bold)
  ```

- **본문은 t5Regular(16px)을 기본으로 사용합니다**

### DON'T

- **t10 이하 크기를 핵심 정보에 사용하지 않습니다**
  ```
  ❌ 가격을 t9Regular(12px)로 표시
  ```

- **한 화면에 4개 이상의 크기 단계를 혼용하지 않습니다**
  ```
  ❌ t1 + t3 + t5 + t7 + t9를 한 카드에 모두 사용
  ```

- **굵기를 남용하지 않습니다**
  ```
  ❌ 카드 내 모든 텍스트를 Bold로 처리
  ✅ 제목만 Bold, 나머지는 Regular/Medium
  ```

---

## 6. Carmore 도메인 활용 예시

### 검색 결과 카드 (ListingCard)

```
차량명 / 숙소명    → $typography.title3     (t3Bold, 20px)
위치 / 주소        → $typography.body2      (t7Regular, 14px)
평점 "4.8 (128)"  → $typography.body2-emphasis (t7Medium, 14px)
가격 "₩45,000/일" → $typography.price      (t5Bold, 16px)
총합 "총 ₩315,000" → $typography.caption1  (t8Regular, 13px)
```

### 예약 확인 다이얼로그

```
타이틀 "예약을 확정할까요?" → $typography.title3     (t3Bold, 20px)
설명문                      → $typography.body1      (t5Regular, 16px)
버튼 라벨 "확인"            → $typography.label1     (t5Bold, 16px)
버튼 라벨 "취소"            → $typography.label1     (t5Bold, 16px)
```
