# nest_study
Nest.js 공부하는 레포   
1. 2023.07.05 - 2023.07.09
기업 백엔드 사전과제를 하며 Nest.js 설치부터 백엔드 구축까지 처음 접해봄.    
모듈화된 아키텍처를 사용하며, 비동기 처리로 스트리밍, 웹소켓 구현에 용이할 것이라고 생각.
해당 프로젝트를 통해 간단한 기능 구현 및 코드 리팩토링을 진행하므로써 Nest.js, typeORM 공부하고자 함.
+ DB 와 상호작용하기 전 로직을 Service or Controller 중 어디 작성하는 것이 일반적인 패턴인지 파악해야 함. 

Service -> Controller -> Module 로 접근 제어   

```typescript
import { Injectable } from '@nestjs/common';
import { AuthGuard } from '@nestjs/passport';

@Injectable()
export class AuthService('access') {

  // 처리할 로직 + DB 와 상호작용을 하는 공간
}
```
 
```typescript
@Controller('auth')
export class AuthController {
  constructor(private readonly authService: AuthService) {} // 의존성 주입

  // url 설정, authService 함수를 호출
}
```
```typescript
// Module 단위로 프로젝트를 관리
@Module({
  imports:[],
  controllers: [AuthController],
  providers: [AuthService, UserService, JwtAccessGuard],
})
export class AuthModule {}
```
