# App Builder Kit

코딩을 몰라도 앱을 만들 수 있는 Claude Code 기반 도구입니다.

## 왜 만들었나요?

> "앱 아이디어는 있는데, 코딩을 모르니까 시작조차 못 하겠어."

이런 사람들을 위해 만들었습니다.

개발 지식이 없어도 **"뭘 만들고 싶은지"만 말하면** Claude가 기획부터 설계, 구현까지 전부 처리합니다. 기술 용어 대신 일상 언어로 소통하고, 모든 기술적 결정은 AI가 내리되 사용자가 이해할 수 있는 말로 확인을 받습니다.

### 핵심 철학

- **기술 용어 없이 소통** — "데이터베이스"가 아니라 "정보 저장소", "API"가 아니라 "서버에 요청하는 방법"
- **매 단계마다 확인** — AI가 혼자 달리지 않습니다. 항상 "이렇게 할게요, 괜찮으세요?"
- **한 번에 하나씩** — 기능 하나를 기획하고, 만들고, 확인하고, 다음으로 넘어갑니다
- **수정도 쉽게** — "이거 바꾸고 싶어"라고 하면 현재 동작을 설명해주고 변경안을 제시합니다

### 기술 기반

프론트엔드에는 [토스(Toss) 오픈소스 생태계](https://github.com/toss)를 기본으로 사용합니다:

- [es-toolkit](https://github.com/toss/es-toolkit) — 유틸리티 (lodash 대체, 2~3배 빠름)
- [overlay-kit](https://github.com/toss/overlay-kit) — 모달/팝업 관리
- [@suspensive/react](https://github.com/toss/suspensive) — Suspense + ErrorBoundary
- [@toss/use-funnel](https://github.com/toss/use-funnel) — 단계별 입력 플로우
- [Tossface](https://toss.im/tossface) — 이모지 폰트 (3,600개)
- [Pretendard](https://github.com/orioncactus/pretendard) — 한글 본문 폰트

## 어떻게 동작하나요?

```
비개발자                        Claude (AI)
  │                               │
  ├─ "앱 만들고 싶어" ──────────→  질문으로 요구사항 파악
  ├─ 답변 ──────────────────────→  프로젝트 생성
  │                               │
  ├─ "로그인 기능 필요해" ──────→  데이터 질문 3단계
  ├─ 답변 ──────────────────────→  기획서 정리 + 확인
  │                               │
  ├─ "만들어줘" ────────────────→  설계 → 확인 → 구현
  ├─ "네" ──────────────────────→  코드 생성 + 결과 설명
  │                               │
  ├─ "닉네임 길이 늘리고 싶어" ─→  현재 동작 설명 → 변경안 제시
  ├─ "네" ──────────────────────→  수정 + 문서 업데이트
```

## 시작하기

### 1. 필요한 것

- 터미널 (맥: Terminal, 윈도우: PowerShell)
- Node.js 18 이상
- Claude Code CLI

### 2. 설치

```bash
# Claude Code 설치
npm install -g @anthropic-ai/claude-code

# 이 저장소 다운로드
git clone https://github.com/shoeone96/app-builder-kit.git
cd app-builder-kit

# Claude 시작
claude
```

### 3. 첫 프로젝트 만들기

Claude가 실행되면 아래처럼 말하면 됩니다:

```
앱 만들고 싶어
```

AI가 물어볼 거예요:
- 앱 이름이 뭐예요?
- 누가 쓰는 앱이에요?
- 이 앱으로 뭘 할 수 있어요?
- 웹으로 볼 건가요, 앱으로도 볼 건가요?

## 사용할 수 있는 명령어

| 명령어 | 용도 | 예시 |
|--------|------|------|
| `/시작` | 새 앱 프로젝트 만들기 | "앱 만들고 싶어", "새 프로젝트" |
| `/기획` | 기능 하나씩 기획 | "로그인 기능 만들고 싶어", "기획하자" |
| `/화면` | 화면 구성 기획 | "로그인 화면 만들자", "메인 화면 기획" |
| `/만들어` | 기획한 걸 코드로 구현 | "만들어줘", "구현해줘" |
| `/바꿔` | 기존 기능 수정 | "이거 바꾸고 싶어", "수정해줘" |
| `/현황` | 진행 상황 확인 | "어디까지 했어?", "현황 보여줘" |
| `/설명해` | 모르는 개념 설명 | "서버가 뭐야?", "이게 뭐야?" |

## 앱 만드는 순서

```
1. /시작  →  프로젝트 만들기
2. /기획  →  기능 하나씩 기획
3. /화면  →  화면 구성
4. /만들어 →  기획한 걸 코드로
5. /바꿔  →  수정하고 싶은 거 수정
6. /현황  →  진행 상황 확인
```

## 프로젝트 구조

```
app-builder-kit/
├── README.md                           # 이 파일
├── .claude/
│   ├── CLAUDE.md                       # AI 소통 규칙 (핵심)
│   ├── settings.local.json             # 퍼미션 설정
│   ├── agents/pm.md                    # 프로덕트 매니저 에이전트
│   ├── skills/                         # 7개 스킬 (명령어)
│   │   ├── 시작/    기획/    화면/
│   │   ├── 만들어/  바꿔/    현황/
│   │   └── 설명해/
│   ├── subagents/                      # 5개 서브에이전트 (자동 호출)
│   │   ├── api-designer/               # API 설계
│   │   ├── data-modeler/               # DB 설계
│   │   ├── backend-builder/            # 서버 코드 생성
│   │   ├── frontend-builder/           # 화면 코드 생성
│   │   └── logic-explainer/            # 코드→기획 번역
│   └── references/                     # 공유 참조 문서
│       ├── communication-guide.md      # 비개발자 소통 규칙
│       ├── tech-stack-options.md       # 기술 스택 선택지
│       └── project-structure-templates.md
└── docs/                               # 자동 생성되는 문서
    ├── features/                       # 기능 기획서
    ├── screens/                        # 화면 기획서
    └── design/                         # 기술 설계서
```

## 팁

- **한 번에 하나씩** — 기능 하나를 기획하고 만들고, 그다음 기능으로 넘어가세요
- **편하게 대답하세요** — 어려운 말 안 써도 돼요
- **"잘 모르겠어"** — 괜찮아요. AI가 선택지를 제안해줄 거예요
- **"다시 해줘"** — 마음에 안 들면 다시 요청하면 돼요
- **PM 에이전트** — 여러 기능을 한 번에 만들고 싶으면 "전체 기능 만들어줘"

## 크레딧

- 이모지: [토스팀에서 제공한 토스페이스](https://toss.im/tossface)
- 폰트: [Pretendard](https://github.com/orioncactus/pretendard)
- 유틸리티: [토스 오픈소스](https://github.com/toss) (es-toolkit, overlay-kit, suspensive, use-funnel)

## 라이선스

MIT License — [LICENSE](LICENSE) 참고
