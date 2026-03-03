# 데이터 모델링 가이드

## 기본 원칙

1. 모든 테이블에 `id` (고유번호), `createdAt` (생성일시), `updatedAt` (수정일시) 포함
2. 테이블명은 영문 소문자 단수형 (user, post, comment)
3. 항목명은 camelCase (firstName, createdAt)
4. 관계는 외래키로 연결

## 항목 타입 매핑

| 기획 표현 | DB 타입 | 예시 |
|----------|---------|------|
| 이메일 | String (unique) | user.email |
| 비밀번호 | String (해시) | user.passwordHash |
| 닉네임 | String (min~max) | user.nickname |
| 긴 글 | Text | post.content |
| 짧은 글 | String | post.title |
| 숫자 | Int / Float | user.age |
| 날짜/시간 | DateTime | user.createdAt |
| 예/아니오 | Boolean | user.isActive |
| 선택지 | Enum | user.role (ADMIN, USER) |
| 이미지 | String (URL) | user.profileImageUrl |

## 관계 패턴

### 1:N (하나 대 여러개)
- 사용자 ↔ 게시글: 사용자 1명이 게시글 여러 개
- 게시글 테이블에 `authorId` → 사용자 테이블 연결

### N:M (여러개 대 여러개)
- 사용자 ↔ 태그: 중간 테이블로 연결 (userTag)

### 1:1 (하나 대 하나)
- 사용자 ↔ 프로필: 각각 하나씩

## 비개발자 확인용 출력 형식

```
📋 저장할 정보 정리

[사용자 정보]
- 이메일 (고유, 중복 불가)
- 비밀번호 (잠금 처리해서 저장)
- 닉네임 (고유, 2~12자)
- 가입일시 (자동 기록)

[게시글 정보]
- 제목 (최대 100자)
- 내용
- 작성자 → 사용자 정보와 연결
- 작성일시 (자동 기록)

연결 관계: 사용자 1명 → 게시글 여러 개
```

## Prisma 스키마 변환 규칙

기획 언어 → Prisma 스키마 자동 변환:
- "고유" → @unique
- "필수" → 기본 (Prisma는 기본이 required)
- "선택" → ? (optional)
- "자동 기록" → @default(now())
- "자동 번호" → @id @default(autoincrement())
