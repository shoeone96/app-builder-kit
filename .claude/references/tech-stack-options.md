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

## 기술 호환성 원칙

스택 선택 시 다음을 자동으로 보장:

1. **공식 문서 우선**: 각 라이브러리의 공식 문서 Getting Started / 권장 패턴을 기본으로 사용
2. **프론트↔백 호환**: 백엔드 인증 방식이 정해지면, 프론트도 그 표준에 맞는 클라이언트 라이브러리 사용
3. **버전 호환**: 주요 라이브러리 간 호환되는 버전 조합 선택 (예: Next.js 14 + NextAuth v5)
4. **생태계 통일**: 한 생태계의 표준을 따르되, 다른 생태계의 패턴을 섞지 않음

### 스택별 표준 조합 참고

| 스택 | 인증 | DB | 프론트 연동 |
|------|------|-----|-----------|
| Next.js | NextAuth.js → 공식 Provider 패턴 | Prisma → 공식 스키마 패턴 | built-in (같은 프레임워크) |
| Express | Passport.js → 공식 Strategy 패턴 | Prisma → 공식 스키마 패턴 | REST 표준 + 토큰 기반 |
| Spring Boot | Spring Security → 공식 SecurityFilterChain | Spring Data JPA → 공식 Repository 패턴 | REST 표준 + OAuth2/JWT |
