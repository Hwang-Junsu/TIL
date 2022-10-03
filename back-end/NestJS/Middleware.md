# Middleware
- 미들웨어는 라우트 핸들러 전에 호출되는 함수입니다 . 미들웨어 기능은 요청 및 응답 객체에 대한 액세스 권한이 next()있으며 애플리케이션의 요청-응답 주기에 있는 미들웨어 기능입니다. 
- Nest 미들웨어는 기본적으로 익스프레스 미들웨어와 동일합니다. 공식 익스프레스 문서의 다음 설명은 미들웨어의 기능에 대해 설명합니다.
> 미들웨어 기능은 다음 작업을 수행할 수 있습니다.    
> 모든 코드를 실행합니다.    
> 요청 및 응답 개체를 변경합니다.    
> 요청-응답 주기를 종료합니다.    
> 스택의 다음 미들웨어 함수를 호출합니다.    
> 현재 미들웨어 함수가 요청-응답 주기를 종료하지 않으면 next()다음 미들웨어 함수에 제어를 전달하기 위해 호출해야 합니다. 그렇지 않으면 요청이 중단됩니다.    

- 함수 또는 @Injectable()데코레이터가 있는 클래스에서 맞춤 Nest 미들웨어를 구현합니다. 
- 클래스는 NestMiddleware인터페이스를 구현해야 하지만 함수에는 특별한 요구 사항이 없습니다. 
- 클래스 메서드를 사용하여 간단한 미들웨어 기능을 구현하는 것으로 시작하겠습니다.

```
import { Injectable, NestMiddleware } from '@nestjs/common';
import { Request, Response, NextFunction } from 'express';

@Injectable()
export class LoggerMiddleware implements NestMiddleware {
  use(req: Request, res: Response, next: NextFunction) {
    console.log('Request...');
    next();
  }
}

```
- Nest 미들웨어는 Dependency Injection을 완벽하게 지원합니다. 
- 공급자 및 컨트롤러와 마찬가지로 동일한 모듈 내에서 사용 가능한 종속성을 주입 할 수 있습니다. 평소와 같이 이 작업은 를 통해 수행됩니다 

# apply Middleware
```
import { Module, NestModule, MiddlewareConsumer } from '@nestjs/common';
import { LoggerMiddleware } from './common/middleware/logger.middleware';
import { CatsModule } from './cats/cats.module';

@Module({
  imports: [CatsModule],
})
export class AppModule implements NestModule {
  configure(consumer: MiddlewareConsumer) {
    consumer
      .apply(LoggerMiddleware)
      .forRoutes('cats');
  }
}
```
- @Module()데코레이터 에는 미들웨어가 들어갈 자리가 없습니다 . configure()대신 모듈 클래스의 메서드를 사용하여 설정합니다. 
- 미들웨어를 포함하는 모듈은 NestModule인터페이스를 구현해야 합니다. LoggerMiddleware수준 에서 설정합시다 AppModule.
