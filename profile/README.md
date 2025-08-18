
<h1>팀 구성원</h1>
<br/>

| Name    | <center>조찬호</center> | <center>김하정</center> | <center>김수미</center> |
| ------- | --------------------------------------------- | ------------------------------------ | ------------------------------------ |
| Profile | <center> <img width="110px" height="110px" src="https://avatars.githubusercontent.com/u/177176591?v=4" /> </center>|<center><img width="110px" height="110px" src="https://avatars.githubusercontent.com/u/178122100?v=4" /></center>|<center><img width="110px" height="110px" src="https://avatars.githubusercontent.com/u/225784309?v=4" /></center>|

# Git 컨벤션 & 프로젝트 운영 규칙

## 1. 커밋 컨벤션

| Type | 설명 |
| --- | --- |
| Feat | 기능 **추가 완료** (새로운 기능 구현) |
| Updated | 기능 **개선/업그레이드** (성능, 최적화 등) |
| Fix | **버그 수정/디버깅** |
| Docs | **문서** 추가/수정 (주석, README, 가이드 등) |
| Style | **코드 스타일/포맷** 변경 (로직 변경 없음) |
| Prototype | **프로토타입/실험** 구현 (초기 탐색) |
| Chore | 빌드/설정/의존성/기타 잡무 |
| Test | **테스트 코드** 추가/수정 |
| Refactor | 내부 구조 개선 (**기능 변화 없음**) |
| Remove | 코드/파일/기능 **삭제** |
| WIP | **중간 저장**(작업 진행 중) — 보호 브랜치 금지, 머지 전 **squash 필수** |
| Branch | **새 브랜치 생성/초기화** 커밋(목적/스코프 명시) |

### 1.1 메시지 형식

```bash
git commit -m "Type YYYY.MM,DD: title" -m "[Body]"

```

- **첫 번째 `m` (헤더)**
    - `Type`: 위 표의 키워드(예: `Feat`, `Fix`, `WIP`, `Branch`, …)
    - `날짜`: `YYYY.MM,DD` (예: `2025.08,18`)
    - `title`: 50자 내외, 한글 OK, 명령형/현재형
- **두 번째 `m` (Body)**
    - **Why**(변경 배경), **What**(주요 변경), **Impact**(영향/마이그레이션) 를 bullet로 기재

### 브레이킹 변경 표기

- 헤더 타입 뒤에 `!` 추가:
    
    `Feat! 2025.08,18: 인증 API 스키마 변경`
    
- 또는 Body에 `BREAKING CHANGE:` 행 추가

### 1.3 예시

**중간 저장(WIP)** — *보호 브랜치 금지, 개인/로컬/개인 원격에서만 허용*

```bash
git commit -m "WIP 2025.08,18: 프로필 편집 초기 UI 뼈대" \
  -m "- 레이아웃 기초
- 상태관리 구조 미정
[skip ci]"

```

**브랜치 생성 기록**

```bash
git commit -m "Branch 2025.08,18: feature/profile-edit 브랜치 생성" \
  -m "- 목적: 프로필 편집 기능 구현
- 스코프: view, api/profile"

```

**기능 추가**

```bash
git commit -m "Feat 2025.08,18: 프로필 저장 API 연동" \
  -m "- POST /api/profile 저장
- 테스트 추가
Resolves: #123"

```

**브레이킹 변경**

```bash
git commit -m "Feat! 2025.08,18: 응답 필드 foo→bar로 변경" \
  -m "BREAKING CHANGE: 클라이언트 필드명 업데이트 필요"

```

## 2. 브랜치 전략

### 2.1 모델

- **보호 브랜치**
    - `main`: **배포 기준**, **직접 커밋 금지**
    - `dev`: **통합 검증**, **직접 커밋 금지**
- **작업 흐름**
    1. `feature/*`(또는 `fix/*` …)에서 작업
    2. PR로 `dev`에 **Squash & Merge**
    3. 검증 완료 시 **릴리스 PR**로 `dev → main` 승격
    4. `main` 병합 후 **태그 부여** 및 **릴리스 노트 게시**
    5. 필요 시 `main → dev` **back-merge**로 동기화

### 2.2 브랜치 네이밍

```
<category>/<scope>-<짧은-설명>

```

- `category`: `feature` | `fix` | `chore` | `refactor` | `test` | `prototype` | `hotfix`
- `scope`: 모듈/도메인 (예: `auth`, `profile`)
- **예시**
    - `feature/profile-edit`
    - `fix/auth-token-refresh`
    - `prototype/ai-suggestion-poc`

### 2.3 생성/동기화

```bash
# 생성
git checkout -b feature/profile-edit

# 원격 추적
git push -u origin feature/profile-edit

# 정기 동기화 (dev 기준)
git fetch origin
git rebase origin/dev    # 충돌은 이 시점에 해결

```

> 릴리스 사이클 후에는 main을 dev로 back-merge 해 기준점 정렬
> 

```bash
git checkout dev
git pull
git merge --ff-only origin/main  # 충돌 시 해결 후 push

```

### 2.4 병합 규칙

- **PR 필수**, **Squash & Merge 기본**(`feature/*` → `dev`)
- `dev → main`은 **“릴리스 PR”**로 진행 (상세는 §4)
- **Rebase 우선**, 머지 커밋 최소화(히스토리 선형 유지)
- 충돌 해결 책임: **브랜치 소유자**

## 3. Pull Request 규칙 (프로젝트 별 선택)

### 3.1 검토 & 권한

- 승인: **최소 2명 (본인 포함)**
- 작성자 본인 병합 가능(승인·CI 충족 시)

### 3.2 품질 게이트

- **빌드/테스트/린트** 모두 통과
- UI 변경: **스크린샷** 첨부
- 브레이킹/마이그레이션 시나리오 **명시**

### 3.3 체크리스트

- [ ]  목적/배경 설명
- [ ]  사용자 영향/릴리스 노트 여부
- [ ]  스크린샷(UI 변경 시)
- [ ]  브레이킹/마이그레이션 안내
- [ ]  테스트 추가/수정 및 수동 시나리오
- [ ]  컨벤션(타입/제목/본문/푸터) 준수
- [ ]  CI 통과
- [ ]  리뷰 코멘트 반영

### 3.4 PR 템플릿

```markdown
## 목적
-

## 주요 변경
-

## 스크린샷 (UI 또는 가시화 가능한 경우)
-

## 테스트
- [ ] 테스트 추가/수정
- [ ] 수동 테스트 시나리오 기재

## 영향도/릴리스 노트
-

## 이슈
- Resolves: #

## 체크리스트
- [ ] 컨벤션(타입/제목/본문/푸터) 준수
- [ ] CI 통과
- [ ] 리뷰 코멘트 반영

```

## 4. 자주 쓰는 명령 모음

```bash
# 최신 dev 기반으로 작업 시작
git checkout dev && git pull
git checkout -b feature/<scope>-<desc>

# 작업 중 정기 동기화
git fetch origin && git rebase origin/dev

# dev → main 릴리스 PR 전 최신화
git checkout dev && git pull
git checkout main && git pull
# (릴리스 PR은 Git 호스팅 UI에서 생성)

# 릴리스 후 동기화
git checkout dev
git pull
git merge --ff-only origin/main
git push

```
