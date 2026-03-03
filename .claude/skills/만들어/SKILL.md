# /만들어 — 기획 → 코드 변환

기획된 기능을 실제 코드로 만드는 스킬.

## 트리거

"만들어줘", "구현해줘", "코딩해줘", "이거 만들어"

## 참조

- `.claude/references/communication-guide.md`
- 관련 subagents: data-modeler, api-designer, backend-builder, frontend-builder

## 실행 흐름

### Step 1: 기능 선택

1. `docs/features/` 폴더 확인
2. 기획서가 여러 개면: "어떤 기능을 만들까요?" + 목록 제시
3. 기획서가 하나면: "이 기능을 만들게요: {기능명}. 맞나요?"
4. 기획서가 없으면: "먼저 기획이 필요해요. `/기획`으로 기능을 정리해볼까요?"

### Step 2: 기획서 확인

선택된 `docs/features/{기능명}.md` 읽기
"기획서를 확인했어요. 이 내용대로 만들게요."

### Step 3: 설계 (subagent 호출)

**a. 데이터 설계** (data-modeler 호출):
- 결과를 기획 언어로 번역:
- "이 정보를 이렇게 정리해서 저장할게요:"
- 표로 보여주기
- "이렇게 하면 될까요?"

**b. API 설계** (api-designer 호출):
- 결과를 기획 언어로 번역:
- "서버에 이런 요청들이 필요해요:"
- "새 사용자 만들기 → 이메일, 비밀번호, 닉네임을 보내면 → 가입 완료 정보를 돌려받아요"
- "이렇게 하면 될까요?"

### Step 4: 구현 (승인 후)

**a. 백엔드** (backend-builder 호출):
- 서버 코드 생성
- DB 스키마 생성

**b. 프론트엔드** (frontend-builder 호출):
- 화면 코드 생성
- 토스 OSS 라이브러리 활용:
  - 오버레이 → overlay-kit
  - 로딩/에러 → @suspensive/react
  - 단계별 플로우 → @toss/use-funnel
  - 유틸리티 → es-toolkit

### Step 5: 완료 보고

"이 기능이 완성됐어요! 이런 파일들이 만들어졌어요:"
- 각 파일의 역할을 한 줄로 설명

### Step 6: 문서 업데이트

- `docs/design/api-spec.md` 업데이트
- `docs/design/data-spec.md` 업데이트
- `docs/progress.md` 업데이트: 📋 기획 완료 → ✅ 완성
