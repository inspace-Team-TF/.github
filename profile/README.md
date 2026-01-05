<h1>팀 구성원</h1>
<br/>

| Name    | <center>조찬호</center> | <center>김하정</center> | <center>김수미</center> |
| ------- | --------------------------------------------- | ------------------------------------ | ------------------------------------ |
| Profile | <center> <img width="110px" height="110px" src="https://avatars.githubusercontent.com/u/177176591?v=4" /> </center>|<center><img width="110px" height="110px" src="https://avatars.githubusercontent.com/u/178122100?v=4" /></center>|<center><img width="110px" height="110px" src="https://avatars.githubusercontent.com/u/225784309?v=4" /></center>|

# [2026] Operations Hub 운영 규칙

## 1. 커밋 컨벤션

| Type | 설명 |
| --- | --- |
| **Feat** | 기능 **추가 완료** (새로운 기능 구현) |
| **Updated** | 기능 **개선/업그레이드** (성능, 최적화 등) |
| **Fix** | **버그 수정/디버깅** |
| **Docs** | **문서** 추가/수정 (주석, README, 가이드 등) |
| **Style** | **코드 스타일/포맷** 변경 (로직 변경 없음) |
| **Prototype** | **프로토타입/실험** 구현 (초기 탐색) |
| **Chore** | 빌드/설정/의존성/기타 잡무 |
| **Refactor** | 내부 구조 개선 (**기능 변화 없음**) |
| **Temp** | **작업 진행 중 중간저장** (WIP에서 명칭 변경) — 머지 전 **squash 필수** |
| **Branch** | **새 브랜치 생성/초기화** 커밋(목적/스코프 명시) |

### 1.1 메시지 형식

```bash
git commit -m "Type YYYY.MM.DD: title" -m "[Body]"

```

* **Type**: 위 표의 키워드 활용
* **날짜**: `YYYY.MM.DD` 형식
* **Body**: Why(배경), What(변경 내용), Impact(영향도)를 불렛 포인트로 기재 (권장)

---

## 2. 브랜치 전략

### 2.1 모델 및 흐름

* **main**: 배포 기준 브랜치 (직접 커밋 금지)
* **dev**: 통합 검증 브랜치 (직접 커밋 금지)
* **작업 흐름**: `feature/*` 작업 → PR 생성 → `dev`에 **Squash & Merge** → 검증 후 `main` 승격

### 2.2 브랜치 네이밍 (권장)

`<category>/<scope>-<짧은-설명>`

* 예: `feature/profile-edit`, `fix/auth-token-refresh`

---

## 3. 프로젝트 관리 및 라벨 (Labels)
> 새 레파지토리 생성시 적용 필요

### 3.1 업무용 라벨 (Development & Planning)

| 라벨 이름 | 설명 (Description) | 추천 색상 |
| --- | --- | --- |
| **Type: Planning** | 기획 및 아이디어 구상 단계의 작업 | `#D4C5F9` |
| **Type: Spec** | 업무의 상세 정의 및 구체화(Specification) 작업 | `#FBCA04` |
| **Type: Feature** | 새로운 기능을 설계하고 개발하는 작업 | `#0E8A16` |
| **Type: Dev** | 전반적인 개발 관련 일반 업무 | `#1D76DB` |
| **Type: Enhancement** | 기존 기능의 성능 개선 및 고도화 작업 | `#5319E7` |
| **Type: Bug** | 예기치 못한 오류 보고 및 버그 수정 | `#D73A4A` |
| **Type: Refactoring** | 기능 변경 없이 코드 품질을 개선하는 작업 | `#006B75` |
| **Type: Fix** | 단순 오타 수정이나 사소한 기능 변경 | `#F9D0C4` |
| **Type: Document** | 매뉴얼, 기술 문서, 업무 보고 등 문서화 작업 | `#0075CA` |

### 3.2 근태 및 운영용 라벨 (Absence & Admin)

| 라벨 이름 | 추천 색상 | 용도 (Description) |
| --- | --- | --- |
| **Type: Leave** | `#E9E9E9` | 연차, 반차, 보상휴가 등 개인 휴가 일정 |
| **Type: Trip** | `#FBCA04` | 외부 미팅, 세미나, 현장 출장 등 외부 활동 |
| **Type: Event** | `#C2E0C6` | 정기 회의, 워크샵, 릴리즈 등 팀 이벤트 |
| **Type: Admin** | `#D4C5F9` | 자산 관리, 서류 제출 등 일반 행정 업무 |
| **Type: Milestone** | `#006B75` | 반드시 완료되어야 하는 중요한 이정표 |

---

## 4. 이슈 템플릿 (Issue Templates)
> 새 레파지토리 생성시 적용 필요

### 템플릿 1: [Project] Planning & Development

* **목적**: 기획, 전략, 개발 및 일반 업무 등록
* **내용**:

```markdown
## 📝 Summary
> (이 작업의 목적과 기대 결과를 간단히 작성)

## 📋 Tasks
- [ ] 
- [ ] 

## 📅 Timeline
- **시작 예정일**: YYYY-MM-DD
- **완료 목표일**: YYYY-MM-DD
*(중단 및 재시작 시 해당 일정도 업데이트 필수)*

## 🔗 관련 정보 (References)
- 관련 이슈: #
- 참고 문서/링크: 

```

### 템플릿 2: [Absence] Leave & Business Trip

* **목적**: 연차, 반차, 출장 등 부재 일정 공유
* **내용**:

```markdown
## 🗓️ 부재 정보 (Details)
- **종류**: (연차 / 반차 / 출장 / 기타)
- **기간**: YYYY-MM-DD ~ YYYY-MM-DD

## 📢 업무 인수인계 (Handover)
- 부재 중 긴급 연락처: 
- 업무 대행자 또는 공유 사항: 

```
