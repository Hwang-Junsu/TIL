# Interceptor
- @Injectable()인터셉터는 데코레이터 로 주석이 달린 클래스 이며 NestInterceptor인터페이스를 구현합니다.

![img](https://docs.nestjs.com/assets/Interceptors_1.png)

- 인터셉터에는 AOP( Aspect Oriented Programming ) 기술 에서 영감을 받은 유용한 기능 세트가 있습니다 . 이를 통해 다음을 수행할 수 있습니다.

> 메서드 실행 전후에 추가 논리 바인딩    
> 함수에서 반환된 결과를 변환    
> 함수에서 throw된 예외를 변환합니다.    
> 기본 기능 동작 확장    
> 특정 조건에 따라 함수를 완전히 재정의합니다(예: 캐싱 목적).    

# example
```
import { Injectable, NestInterceptor, ExecutionContext, CallHandler } from '@nestjs/common';
import { Observable } from 'rxjs';
import { tap } from 'rxjs/operators';

@Injectable()
export class LoggingInterceptor implements NestInterceptor {
  intercept(context: ExecutionContext, next: CallHandler): Observable<any> {
    console.log('Before...');

    const now = Date.now();
    return next
      .handle()
      .pipe(
        tap(() => console.log(`After... ${Date.now() - now}ms`)),
      );
  }
}
```
