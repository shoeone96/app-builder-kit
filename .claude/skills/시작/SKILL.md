# /시작 — 새 앱 프로젝트 시작

처음 앱을 만들 때 프로젝트를 세팅하는 스킬.

## 트리거

"앱 만들고 싶어", "새 프로젝트", "시작하자", "앱 하나 만들자"

## 참조

- `.claude/references/tech-stack-options.md`
- `.claude/references/project-structure-templates.md`
- `.claude/references/communication-guide.md`

## 실행 흐름

### Step 1: 기본 정보 수집

순서대로 하나씩 질문:

1. "앱 이름을 뭘로 할까요? (예: 우리동네맛집, 공부친구)"
2. "누가 쓰는 앱이에요? (예: 대학생, 직장인, 누구나)"
3. "이 앱으로 뭘 할 수 있어요? 3가지만 말해주세요"
   - 잘 모르겠다고 하면 예시 제시: "예를 들어, 맛집 앱이면: 맛집 찾기, 리뷰 쓰기, 즐겨찾기"
4. "웹으로 볼 건가요, 앱(폰)으로도 볼 건가요?"
   - "잘 모르겠어요" → "일단 웹으로 시작할게요. 나중에 앱도 만들 수 있어요"

### Step 2: 기술 스택 자동 결정

`tech-stack-options.md` 참조하여 자동 선택. 사용자에게는:
- "이 앱에 맞는 도구들을 준비할게요."
- "잘 만들어진 도구들을 기본으로 쓸 거예요." (토스 OSS 언급 불필요)

### Step 3: 프로젝트 생성

`project-structure-templates.md` 참조하여 폴더 구조 생성:
1. 선택된 템플릿에 맞는 폴더/파일 생성
2. package.json에 토스 OSS 라이브러리 포함:
   - es-toolkit
   - overlay-kit
   - @suspensive/react
   - @toss/use-funnel
3. Tossface 폰트 파일 다운로드 및 배치
4. Pretendard 폰트 CDN 설정
5. `npm install` (또는 `pnpm install`) 실행

### Step 4: 기획 문서 생성

`docs/app-brief.md` 생성:

```markdown
# {앱 이름}

## 한 줄 설명
{사용자 답변 기반}

## 대상 사용자
{Step 1-2 답변}

## 핵심 기능
1. {기능 1}
2. {기능 2}
3. {기능 3}

## 플랫폼
{웹 / 웹+모바일}

## 진행 상태
- [ ] 기능 1 — 기획 전
- [ ] 기능 2 — 기획 전
- [ ] 기능 3 — 기획 전
```

`docs/progress.md` 초기화:

```markdown
# 진행 현황

## ✅ 완성된 기능
(아직 없음)

## 🔨 만드는 중
(아직 없음)

## 📋 기획 예정
- 기능 1
- 기능 2
- 기능 3
```

### Step 5: 완료 안내

"프로젝트가 준비됐어요! 이제 첫 번째 기능을 기획해볼까요? `/기획`을 입력하거나, '기능 기획하자'라고 말해주세요."
