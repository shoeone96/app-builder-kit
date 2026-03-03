# REST API 설계 표준

## URL 규칙

- 자원 중심 복수형: `/api/{자원s}`
- 계층: `/api/users/{id}/posts`
- 동사 금지 (GET /api/users ← 올바름, GET /api/getUsers ← 금지)
- 소문자 + 하이픈: `/api/user-profiles`

## HTTP 메서드 매핑

| 동작 | 메서드 | URL 예시 | 설명 |
|------|--------|---------|------|
| 목록 보기 | GET | /api/users | 전체 목록 |
| 상세 보기 | GET | /api/users/:id | 하나 상세 |
| 만들기 | POST | /api/users | 새로 생성 |
| 수정하기 | PATCH | /api/users/:id | 일부 수정 |
| 삭제하기 | DELETE | /api/users/:id | 삭제 |

## 응답 포맷

### 성공 (단건)
```json
{
  "data": {
    "id": "1",
    "email": "user@example.com",
    "nickname": "사용자"
  }
}
```

### 성공 (목록 + 페이지네이션)
```json
{
  "data": [...],
  "pagination": {
    "cursor": "abc123",
    "hasNext": true
  }
}
```

### 에러
```json
{
  "error": {
    "code": "DUPLICATE_EMAIL",
    "message": "이미 사용 중인 이메일이에요"
  }
}
```

## 상태 코드

| 코드 | 의미 | 사용 |
|------|------|------|
| 200 | 성공 | 조회, 수정, 삭제 성공 |
| 201 | 만들기 성공 | POST 성공 |
| 400 | 잘못된 요청 | 입력값 오류 |
| 401 | 로그인 필요 | 미인증 |
| 403 | 권한 없음 | 접근 불가 |
| 404 | 없음 | 자원 없음 |
| 409 | 충돌 | 중복 (이메일, 닉네임) |
| 500 | 서버 오류 | 내부 에러 |

## 에러 코드 네이밍

- `DUPLICATE_{항목}`: 중복 (DUPLICATE_EMAIL, DUPLICATE_NICKNAME)
- `INVALID_{항목}`: 유효하지 않음 (INVALID_PASSWORD)
- `NOT_FOUND_{자원}`: 없음 (NOT_FOUND_USER)
- `UNAUTHORIZED`: 로그인 필요
- `FORBIDDEN`: 권한 없음

## 입력 유효성 검증

- 이메일: 이메일 형식
- 비밀번호: 최소 8자
- 문자열: 최소/최대 길이
- 필수 항목: required
