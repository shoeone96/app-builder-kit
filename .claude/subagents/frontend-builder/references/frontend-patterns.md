# 프론트엔드 코드 패턴

## 토스 OSS 필수 사용

### es-toolkit (유틸리티)
```typescript
// lodash 대신 es-toolkit 사용
import { groupBy, sortBy, uniq, chunk } from 'es-toolkit';
import { debounce, throttle } from 'es-toolkit';
import { pick, omit } from 'es-toolkit';
```

### overlay-kit (오버레이 관리)
```typescript
// 모달, 팝업, 바텀시트 등
import { overlay } from 'overlay-kit';

// 확인 모달 열기
const confirmed = await overlay.openAsync(({ isOpen, close }) => (
  <ConfirmDialog
    open={isOpen}
    onConfirm={() => close(true)}
    onCancel={() => close(false)}
    title="정말 삭제할까요?"
  />
));

if (confirmed) {
  await deleteItem(id);
}
```

### @suspensive/react (Suspense + ErrorBoundary)
```typescript
import { Suspense, ErrorBoundary } from '@suspensive/react';

function UserList() {
  return (
    <ErrorBoundary fallback={<ErrorMessage />}>
      <Suspense fallback={<Loading />}>
        <UserListContent />
      </Suspense>
    </ErrorBoundary>
  );
}
```

### @toss/use-funnel (단계별 플로우)
```typescript
import { useFunnel } from '@toss/use-funnel';

function SignupPage() {
  const funnel = useFunnel(['이메일', '비밀번호', '닉네임', '완료']);

  return (
    <funnel.Render
      이메일={({ history }) => (
        <EmailStep onNext={(email) => history.push('비밀번호', { email })} />
      )}
      비밀번호={({ context, history }) => (
        <PasswordStep
          email={context.email}
          onNext={(password) => history.push('닉네임', { ...context, password })}
        />
      )}
      // ...
    />
  );
}
```

### Tossface (이모지)
```css
/* globals.css에서 Tossface 폰트 등록 */
@font-face {
  font-family: 'Tossface';
  src: url('/fonts/tossface.ttf') format('truetype');
}

/* 이모지가 필요한 곳에서 사용 */
.emoji {
  font-family: 'Tossface', sans-serif;
}
```

## 컴포넌트 패턴

### function declaration 사용
```typescript
// Good
function UserCard({ user }: UserCardProps) {
  return <div>...</div>;
}

// Bad (arrow function)
const UserCard = ({ user }: UserCardProps) => { ... };
```

### 4가지 UI 상태 필수
```typescript
function UserList() {
  return (
    <ErrorBoundary fallback={<ErrorFallback />}>
      <Suspense fallback={<LoadingSkeleton />}>
        <UserListContent />
      </Suspense>
    </ErrorBoundary>
  );
}

function UserListContent() {
  const { data: users } = useSuspenseQuery(...);

  if (users.length === 0) return <EmptyState message="아직 사용자가 없어요" />;
  return <ul>{users.map(user => <UserCard key={user.id} user={user} />)}</ul>;
}
```

## 스타일 패턴

### Tailwind CSS
```typescript
// 조건부 클래스
import { cn } from '@/lib/utils';

function Button({ variant, children }: ButtonProps) {
  return (
    <button className={cn(
      'px-4 py-2 rounded-lg font-medium',
      variant === 'primary' && 'bg-blue-600 text-white',
      variant === 'secondary' && 'bg-gray-100 text-gray-800',
    )}>
      {children}
    </button>
  );
}
```

### Pretendard 폰트 설정
```css
@font-face {
  font-family: 'Pretendard';
  src: url('https://cdn.jsdelivr.net/gh/orioncactus/pretendard/dist/web/variable/pretendardvariable.css');
}

body {
  font-family: 'Pretendard', -apple-system, sans-serif;
}
```

## 코드 생성 후 설명 형식

```
📁 만들어진 파일들

[화면 쪽]
- src/pages/LoginPage.tsx → 로그인 화면
- src/components/LoginForm.tsx → 로그인 입력 폼
- src/hooks/useLogin.ts → 로그인 처리 기능
```
