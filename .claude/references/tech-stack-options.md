# 기술 스택 선택지

/시작 스킬이 참조. 사용자에게는 기술 이름을 노출하지 않고 특성으로 설명.

## 공통 필수 라이브러리 (토스 OSS 생태계)

모든 옵션에 기본 포함되는 토스 오픈소스:

| 라이브러리 | 용도 | 라이선스 |
|-----------|------|---------|
| es-toolkit | 유틸리티 (lodash 대체, 2~3배 빠름, 97% 작음) | MIT |
| overlay-kit | 모달/팝업/바텀시트 오버레이 관리 | MIT |
| @suspensive/react | Suspense + ErrorBoundary 처리 | MIT |
| @toss/use-funnel | 단계별 입력 플로우 (가입, 설정 등) | MIT |

### 디자인 에셋

| 에셋 | 용도 | 비고 |
|------|------|------|
| Tossface | 이모지 폰트 (3,600개, 일관된 디자인) | 출처 표시 필수 |
| Pretendard | 한글/영문 본문 폰트 | OFL 무료 |

## 옵션 1: 웹 앱 (기본 추천)

**사용자 설명**: "웹사이트 형태 — 브라우저에서 바로 사용"

**기술 스택**:
- 프레임워크: Next.js 14+ (App Router)
- 언어: TypeScript
- DB: PostgreSQL + Prisma ORM
- 인증: NextAuth.js (Google/카카오)
- 스타일: Tailwind CSS
- 배포: Vercel (무료 티어)
- 유틸: es-toolkit, overlay-kit, @suspensive/react, @toss/use-funnel
- 이모지: Tossface
- 폰트: Pretendard

**선택 기준**: 빠르게, 웹만, 복잡한 서버 로직 없을 때

## 옵션 2: 별도 서버 필요

**사용자 설명**: "서버를 따로 두는 앱 — 복잡한 기능이 많을 때"

### 2-A: Node.js 서버
- 백엔드: Express.js + TypeScript
- 프론트: React + Vite + TypeScript
- DB: PostgreSQL + Prisma ORM
- 인증: Passport.js
- 스타일: Tailwind CSS
- 유틸: es-toolkit, overlay-kit, @suspensive/react, @toss/use-funnel
- 배포: Railway(서버) + Vercel(프론트)

### 2-B: Kotlin/Spring 서버
- 백엔드: Spring Boot + Kotlin
- 프론트: React + Vite + TypeScript
- DB: PostgreSQL + Spring Data JPA
- 인증: Spring Security + OAuth2
- 스타일: Tailwind CSS
- 유틸: es-toolkit, overlay-kit, @suspensive/react, @toss/use-funnel
- 배포: Railway(서버) + Vercel(프론트)

**선택 기준**: 복잡한 서버 로직, 모바일 계획, 여러 서비스 연동

## 옵션 3: 모바일 포함

**사용자 설명**: "웹 + 모바일 앱 — 폰에서도 사용"

- 백엔드: Express.js or Spring Boot
- 웹+모바일: React Native (Expo)
- DB: PostgreSQL
- 배포: Railway(서버) + Expo EAS(앱)

## 스택 결정 로직

```
"웹만" → 옵션 1 (Next.js)
"앱도" → 옵션 3 (Expo)
"잘 모르겠어요" → 옵션 1 추천 + "나중에 앱도 만들 수 있어요"
복잡한 서버 로직 필요 → 옵션 2 (Node.js 기본)
```

## 공통 도구 (모든 옵션)

- ESLint + Prettier (코드 정리)
- Git (버전 관리)
- dotenv (설정값 관리)
- es-toolkit (유틸리티)
- Tossface + Pretendard (디자인 에셋)
