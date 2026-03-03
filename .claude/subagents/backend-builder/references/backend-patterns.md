# 백엔드 코드 패턴

## 프로젝트 공통

### 공식 문서 기반 개발 원칙
- 모든 라이브러리 사용법은 해당 버전의 **공식 문서 권장 패턴**을 따른다
- 프론트엔드와 호환되는 표준 방식으로 구현한다 (인증, API 포맷 등)
- 커뮤니티 관행보다 공식 가이드를 우선한다

### 토스 OSS 활용
- es-toolkit: 유틸리티 함수 (lodash 대신 필수 사용)
  - 배열: chunk, uniq, groupBy, sortBy
  - 객체: pick, omit, merge
  - 함수: debounce, throttle

## Next.js API Routes 패턴 (옵션 1)

### Route Handler
```typescript
// src/app/api/users/route.ts
import { NextRequest, NextResponse } from 'next/server';
import { prisma } from '@/lib/db';

export async function GET() {
  const users = await prisma.user.findMany();
  return NextResponse.json({ data: users });
}

export async function POST(request: NextRequest) {
  const body = await request.json();
  // 유효성 검증
  // 비즈니스 로직
  // 응답
}
```

### Prisma 스키마
```prisma
model User {
  id        Int      @id @default(autoincrement())
  email     String   @unique
  password  String
  nickname  String   @unique
  createdAt DateTime @default(now())
  updatedAt DateTime @updatedAt
  posts     Post[]
}
```

## Express 패턴 (옵션 2-A)

### Controller
```typescript
// src/auth/controller.ts
import { Router } from 'express';
import { authService } from './service';

const router = Router();

router.post('/api/users', async (req, res) => {
  const result = await authService.register(req.body);
  res.status(201).json({ data: result });
});

export default router;
```

### Service
```typescript
// src/auth/service.ts
import { prisma } from '../lib/db';
import { hashPassword } from '../lib/crypto';

export const authService = {
  async register(input: RegisterInput) {
    const exists = await prisma.user.findUnique({ where: { email: input.email } });
    if (exists) throw new ConflictError('DUPLICATE_EMAIL');

    return prisma.user.create({
      data: {
        email: input.email,
        password: await hashPassword(input.password),
        nickname: input.nickname,
      },
    });
  },
};
```

## 에러 처리

```typescript
// src/lib/errors.ts
export class AppError extends Error {
  constructor(public code: string, message: string, public statusCode: number) {
    super(message);
  }
}

export class ConflictError extends AppError {
  constructor(code: string) {
    super(code, '이미 존재합니다', 409);
  }
}

export class NotFoundError extends AppError {
  constructor(code: string) {
    super(code, '찾을 수 없습니다', 404);
  }
}
```

## 코드 생성 후 설명 형식

```
📁 만들어진 파일들

[서버 쪽]
- src/auth/controller.ts → 로그인/회원가입 요청을 받는 곳
- src/auth/service.ts → 실제 처리하는 곳
- src/auth/types.ts → 정보 구조 정의
- prisma/schema.prisma → 저장 정보 구조

이 파일들이 함께 동작해서 회원가입 기능이 돌아가요.
```
