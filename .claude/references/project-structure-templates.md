# 프로젝트 구조 템플릿

/시작 스킬이 프로젝트 생성 시 참조.

## 템플릿 1: Next.js 풀스택

```
{프로젝트명}/
├── src/
│   ├── app/                    # 화면들 (페이지)
│   │   ├── layout.tsx          # 공통 화면 틀
│   │   ├── page.tsx            # 첫 화면 (메인)
│   │   ├── login/
│   │   │   └── page.tsx
│   │   └── api/                # 서버 요청 처리
│   │       └── auth/
│   │           └── route.ts
│   ├── components/             # 재사용 화면 조각
│   │   ├── ui/                 # 기본 조각 (버튼, 입력칸)
│   │   └── layout/             # 틀 조각 (헤더, 푸터)
│   ├── lib/                    # 도구 모음
│   │   ├── db.ts               # 정보 저장소 연결
│   │   └── auth.ts             # 로그인 설정
│   └── types/                  # 정보 구조 정의
├── prisma/
│   └── schema.prisma           # 저장 정보 구조
├── public/                     # 이미지, 아이콘
│   └── fonts/
│       └── tossface.ttf        # 토스페이스 이모지 폰트
├── docs/
│   ├── app-brief.md
│   ├── features/
│   ├── screens/
│   ├── design/
│   └── progress.md
├── .env.local
├── package.json
├── tsconfig.json
├── tailwind.config.ts
└── next.config.ts
```

## 템플릿 2: React + Express (분리형)

```
{프로젝트명}/
├── client/                     # 화면 쪽
│   ├── src/
│   │   ├── pages/
│   │   ├── components/
│   │   │   ├── ui/
│   │   │   └── layout/
│   │   ├── hooks/
│   │   ├── services/
│   │   ├── types/
│   │   └── utils/
│   ├── public/
│   │   └── fonts/
│   │       └── tossface.ttf
│   ├── package.json
│   ├── tsconfig.json
│   ├── tailwind.config.ts
│   └── vite.config.ts
├── server/                     # 서버 쪽
│   ├── src/
│   │   ├── routes/
│   │   ├── services/
│   │   ├── models/
│   │   ├── middleware/
│   │   └── utils/
│   ├── prisma/
│   │   └── schema.prisma
│   ├── package.json
│   └── tsconfig.json
├── docs/
│   ├── app-brief.md
│   ├── features/
│   ├── screens/
│   ├── design/
│   └── progress.md
├── .env
└── README.md
```

## 템플릿 3: React + Spring Boot (분리형)

```
{프로젝트명}/
├── frontend/                   # 화면 쪽
│   ├── src/
│   │   ├── pages/
│   │   ├── components/
│   │   │   ├── ui/
│   │   │   └── layout/
│   │   ├── hooks/
│   │   ├── services/
│   │   ├── types/
│   │   └── utils/
│   ├── public/
│   │   └── fonts/
│   │       └── tossface.ttf
│   ├── package.json
│   ├── tsconfig.json
│   ├── tailwind.config.ts
│   └── vite.config.ts
├── backend/                    # 서버 쪽
│   ├── src/main/kotlin/
│   │   └── com/{그룹}/{프로젝트}/
│   │       ├── domain/
│   │       ├── application/
│   │       ├── adapter/
│   │       │   ├── in/web/
│   │       │   └── out/persistence/
│   │       └── config/
│   ├── src/main/resources/
│   │   └── application.yml
│   ├── build.gradle.kts
│   └── settings.gradle.kts
├── docs/
└── README.md
```

## 템플릿 4: Expo (모바일 포함)

```
{프로젝트명}/
├── app/                        # 화면 (Expo Router)
│   ├── (tabs)/
│   │   ├── index.tsx
│   │   └── profile.tsx
│   ├── login.tsx
│   └── _layout.tsx
├── components/
│   ├── ui/
│   └── layout/
├── hooks/
├── services/
├── types/
├── utils/
├── assets/
│   └── fonts/
│       └── tossface.ttf
├── server/
├── docs/
├── app.json
├── package.json
└── tsconfig.json
```

## 선택 가이드

| 사용자 답변 | 템플릿 |
|------------|--------|
| "웹만" + 단순 기능 | 템플릿 1 (Next.js) |
| "웹만" + 복잡 기능 | 템플릿 2 (React + Express) |
| "웹만" + Spring 선호 | 템플릿 3 (React + Spring Boot) |
| "앱도" | 템플릿 4 (Expo) + 서버 |

## docs/ 폴더 (공통)

```
docs/
├── app-brief.md            # 앱 개요
├── features/               # 기능 기획서
├── screens/                # 화면 기획서
├── design/                 # 기술 설계서
│   ├── api-spec.md
│   └── data-spec.md
└── progress.md             # 진행 현황
```
