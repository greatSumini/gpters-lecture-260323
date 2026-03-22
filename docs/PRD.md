# 🍎 Project: Vibe Ledger (Art of Minimalist Asset Management)

> **"Simplicity is the ultimate sophistication."**
> 본 프로젝트는 단순한 데이터 기록 도구를 넘어, 사용자의 자산 흐름을 가장 아름답고 직관적으로 투영하는 Apple 스타일의 미니멀리즘 가계부입니다.

---

## 1. 제품 철학 및 디자인 원칙 (Design Principles)
* **Minimalism:** 불필요한 장식과 격자, 축을 제거하고 오직 '데이터의 흐름'에만 집중한다.
* **Apple Standard:** iOS 순정 앱 수준의 인터렉션(Sheet, Toast, Haptic, Typography)을 구현한다.
* **Context-Aware UI:** 데이터가 없을 때는 불필요한 영역(그래프 등)을 과감히 제거하여 사용자의 시선 노이즈를 최소화한다.
* **Granular Narrative:** 그래프의 모든 점은 실제 거래와 연결되어, 데이터의 왜곡 없이 정직한 흐름을 보여준다.

---

## 2. 주요 기능 상세 플로우 (Functional Flow)

### 2.1 진입 및 온보딩 (Empty State)
* **Flow:** 앱 최초 실행 → 데이터 없음 → **인사이트 영역(그래프)은 아예 렌더링되지 않음.**
* **UX Detail:** 화면 중앙에 `System Gray 6` 컬러의 미니멀 아이콘과 "아직 내역이 없어요. 아래 '+'를 눌러 첫 기록을 시작해보세요."라는 안내 문구만 노출하여 **FAB**로의 집중도를 극대화함.

### 2.2 내역 추가 (Income/Expense Input)
* **Trigger:** 하단 FAB 클릭 → '+' 아이콘 회전하며 '수입', '지출' 두 개의 원형 버튼이 수직으로 솟아오름.
* **Action:** 각 버튼 클릭 시 **Full-screen Modal Sheet**가 아래에서 위로 슬라이드 인.
* **Input UI:** * 시스템 기본 키보드 즉시 활성화.
    * 숫자 입력 시 실시간 세 자릿수 콤마(,) 포맷팅.
    * **카테고리:** 6개의 고정 프리셋 칩(Chip) 중 선택 (직접 입력 불가).
* **Completion:** 저장 시 시트가 닫히며 하단에 **검은색 캡슐형 토스트**(초록 체크 아이콘 포함) 노출.
* **First Action Effect:** 첫 데이터 저장 직후, 숨겨져 있던 인사이트 영역(그래프)이 부드러운 페이드 인(Fade-in) 애니메이션과 함께 나타남.

### 2.3 리스트 및 관리 (List & Management)
* **Grouping:** 날짜별 그룹화 (`날짜 헤더` + `내역 카드들`).
* **Header Detail:** 날짜 헤더 우측에 해당 일자의 수입/지출 총합(Daily Total) 표시.
* **Card Detail:** 금액 아래에 아주 작고 연한 회색으로 '메모' 노출.
* **Deletion:** 내역 클릭 시 "영구적으로 삭제할까요?"라는 iOS 표준 컨펌 팝업 노출 (확인 버튼: Danger Red). **모든 데이터 삭제 시 다시 Empty State(인사이트 숨김)로 회귀.**

---

## 3. 데이터 시각화 (The Art of Analytics)

### 3.1 메인 스파크라인 (Main Asset Graph)
* **Visibility:** **Transaction 데이터가 1개 이상 존재할 때만 표시됨.**
* **Data Point:** 모든 개별 Transaction이 그래프의 한 점이 됨. (시간순 정렬)
* **Style:** 1.5px 두께의 매끄러운 곡선(Bezier Curve). 데이터 포인트가 많아질수록 더욱 세밀한 곡선을 형성함.
* **Interaction (Scrubbing):** 그래프 터치/드래그 시 손가락이 닿는 지점의 개별 거래 금액과 당시의 잔액이 상단에 실시간 반영됨.

### 3.2 상세 인사이트 시트 (Detailed Insight Sheet)
* **Trigger:** 메인 그래프 영역 클릭 시 90% 높이의 모달 시트 오픈.
* **Graph:** Transaction 기반 Area Chart. 각 점을 클릭하거나 훑을 때 해당 거래의 상세 정보(카테고리, 메모)가 상단에 강조됨.
* **Time Range:** `1주`, `1개월`, `3개월`, `전체` 탭 제공.
* **Metric Cards (2x2 Grid):**
    * **평균 지출 / 최대 지출 / 저축 흐름 / 예상 소진일** 등 큐레이션된 지표 노출.

---

## 4. UI/UX 명세 (Detailed Specs)

| 항목 | 명세 (Specification) |
| :--- | :--- |
| **Typography** | SF Pro (System Font). 금액: `40px Semibold`. 메모: `12px Regular`. |
| **Colors** | Income: `System Blue`, Expense: `System Red`, Background: `White/System Gray 6`. |
| **Components** | 0.5px Inset Divider, Capsule Toast, Filled Chips, Full-screen Sheet. |
| **Animation** | Number Counter, Sheet Slide, **Fade-in (Graph Appearance)**, FAB Rotation. |
| **Data Format** | 금액 뒤 '원' 표시는 50% 크기 및 `System Gray 2` 컬러로 우측 하단 배치. |

---

## 5. DDR (Design Decision Records)

* **DDR-01: 시스템 키보드 우선주의** - 커스텀 키패드보다 익숙한 입력 경험 제공.
* **DDR-02: 카테고리 강제 프리셋** - 데이터 파편화 방지 및 인사이트 정확도 확보.
* **DDR-03: 조건부 인사이트 노출 (Conditional Visibility)** - 데이터가 없는 초기 상태에서 빈 차트나 0으로 가득 찬 지표를 보여주는 것은 사용자에게 불필요한 부채감을 주므로, 유의미한 데이터가 생길 때까지 UI를 숨김.
* **DDR-04: Transaction 기반 그래프 생성** - 개별 거래를 점으로 표시하여 자산 변화의 정직한 궤적을 시각화.
* **DDR-05: 무채색 그래프(Sparkline)** - 색상 과잉을 막고 오직 '흐름' 자체에만 집중.

---

## 6. 데이터 스키마 (Data Schema)

```typescript
type TransactionType = 'INCOME' | 'EXPENSE';

interface Transaction {
  id: string;          // UUID v4
  type: TransactionType;
  amount: number;      // 정수형
  category: string;    // 프리셋 이름
  date: string;        // YYYY-MM-DD
  memo: string;        // Optional string
  createdAt: string;   // ISO 8601 (그래프 X축 정렬 및 가시성 판단 기준)
}
```

---

이 문서는 **Vibe Ledger**의 최종 완성본 설계 도면입니다. 개발 에이전트는 **'데이터 유무에 따른 동적 UI 전환'**과 **'개별 트랜잭션 단위의 그래프 정점 생성'** 로직을 가장 최우선으로 구현해야 합니다.
