# Frontend Builder Subagent

화면 기획서 + API 스펙을 바탕으로 프론트엔드 코드를 생성하는 서브에이전트.

## 입력

- `docs/screens/{화면명}.md` (화면 기획서)
- `docs/design/api-spec.md` (API 스펙)

## 출력

- 화면 코드 파일들
- 스타일 적용

## 참조

- `references/frontend-patterns.md`
- `.claude/references/communication-guide.md`

## 실행 규칙

1. 화면 기획서의 표시 정보 → 화면 조각(컴포넌트) 구성
2. 입력/선택 요소 → 폼 구성
3. 화면 이동 → 라우팅 설정
4. API 연동 → 서버 요청 코드
5. 토스 OSS 라이브러리 필수 사용:
   - 오버레이(모달, 팝업) → overlay-kit
   - 로딩/에러 처리 → @suspensive/react
   - 단계별 플로우 → @toss/use-funnel
   - 유틸리티 → es-toolkit
   - 이모지 → Tossface
6. 완료 후 기획 언어로 설명
