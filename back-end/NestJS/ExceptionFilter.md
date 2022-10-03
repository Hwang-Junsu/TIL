# ExceptionFilter
Nest에는 애플리케이션 전체에서 처리되지 않은 모든 예외를 처리하는 예외 레이어 가 내장되어 있습니다.    
애플리케이션 코드에서 예외를 처리하지 않으면 이 계층에서 예외를 포착한 다음 자동으로 적절한 사용자 친화적인 응답을 보냅니다.    

![img](https://docs.nestjs.com/assets/Filter_1.png)

# HttpException
- HttpException생성자는 응답을 결정하는 두 개의 필수 인수를 취합니다 .

- response인수는 JSON 응답 본문을 정의합니다 . string 또는 object아래에 설명된 대로 일 수 있습니다 .
- status인수는 HTTP 상태 코드를 정의합니다 .
- 기본적으로 JSON 응답 본문에는 두 가지 속성이 포함됩니다.
- statusCodestatus: 기본값은 인수 에 제공된 HTTP 상태 코드입니다.
- message: HTTP 오류에 대한 간략한 설명status
- JSON 응답 본문의 메시지 부분만 재정의하려면 response인수에 문자열을 제공합니다. 전체 JSON 응답 본문을 재정의하려면 response인수에 개체를 전달합니다. Nest는 객체를 직렬화하고 JSON 응답 본문으로 반환합니다.
- 두 번째 생성자 인수 - status-는 유효한 HTTP 상태 코드여야 합니다. 모범 사례는 에서 HttpStatus가져온 열거형 을 사용하는 것 @nestjs/common입니다.

```
@Get()
async findAll() {
  throw new HttpException({
    status: HttpStatus.FORBIDDEN,
    error: 'This is a custom message',
  }, HttpStatus.FORBIDDEN);
 ```
 
 # Exception Filter Code
 ```
 import { ExceptionFilter, Catch, ArgumentsHost, HttpException } from '@nestjs/common';
import { Request, Response } from 'express';

@Catch(HttpException)
export class HttpExceptionFilter implements ExceptionFilter {
  catch(exception: HttpException, host: ArgumentsHost) {
    const ctx = host.switchToHttp();
    const response = ctx.getResponse<Response>();
    const request = ctx.getRequest<Request>();
    const status = exception.getStatus();

    response
      .status(status)
      .json({
        statusCode: status,
        timestamp: new Date().toISOString(),
        path: request.url,
      });
  }
}
```
- 기본(내장) 예외 필터가 자동으로 많은 경우를 처리할 수 있지만 예외 레이어를 완전히 제어 할 수 있습니다. 
- 예를 들어, 일부 동적 요소를 기반으로 로깅을 추가하거나 다른 JSON 스키마를 사용할 수 있습니다. 예외 필터 는 정확히 이러한 목적을 위해 설계되었습니다. 
- 이를 통해 정확한 제어 흐름과 클라이언트로 다시 전송되는 응답 내용을 제어할 수 있습니다.
- 클래스 의 인스턴스인 예외를 포착하고 이에 대한 HttpException사용자 정의 응답 로직을 구현하는 예외 필터를 생성해 보겠습니다. 
- 이렇게 하려면 기본 플랫폼 Request과 Response개체에 액세스해야 합니다. Request원본 url을 가져와 로깅 정보에 포함 할 수 있도록 개체 에 액세스합니다 . 
- Response메서드 를 사용하여 전송되는 응답을 직접 제어하기 위해 개체를 사용 합니다 response.json().

## Controller에 적용
```
@Post()
@UseFilters(HttpExceptionFilter)
async create(@Body() createCatDto: CreateCatDto) {
  throw new ForbiddenException();
}
```
