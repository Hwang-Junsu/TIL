# Controller

- 컨트롤러는 들어오는 request를 처리하고 클라이언트에 response를 return하는 역할을 한다.
- 기본 컨트롤러를 만들기 위해서는 클래스와 데코레이터를 사용한다. 데코레이터는 클래스를 필수 메타데이터와 연결하고 Nest가 라우팅 맵을 생성할 수 있도록 한다.

## Example Code
```
import { Controller, Get, Post } from '@nestjs/common';
import { Request } from 'express';
@Controller('cats')
export class CatsController {
  @Post()
  create(): string {
    return 'This action adds a new cat';
  }

  @Get()
  findAll(@Req() request: Request): string {
    return 'This action returns all cats';
  }
}
```

## Routing
- 기본 컨트롤러를 정의하는데 필요한 @Controller()를 사용한다. 데코레이터에서 path를 사용하면 path들을 쉽게 그룹화하고 반복적인 코드를 최소화 할 수 있다.
`CLI를 사용하여 컨트롤러를 생성하려면 $ nest g controller cats명령을 실행하기만 하면 됩니다.`   
    
## Request Object
- 핸들러는 종종 클라이언트 요청 세부정보에 접근해야 한다. Nest는 기본 플랫폼의 Request object에 대한 엑세스를 제공한다.(Express)
- `Req()` 데코레이터를 추가하여 요청개체를 삽입하도록 Nest에게 지시하여 엑세스 할 수 있다.
> @Request(), @Req()	req
> @Response(), @Res()*	res    
> @Next()	next    
> @Session()	req.session    
> @Param(key?: string)	req.params/req.params[key]    
> @Body(key?: string)	req.body/req.body[key]    
> @Query(key?: string)	req.query/req.query[key]    
> @Headers(name?: string)	req.headers/req.headers[name]    
> @Ip()	req.ip    
> @HostParam()	req.hosts    

## Status Code
```
@Post()
@HttpCode(204)
create() {
  return 'This action adds a new cat';
}
```
- 응답 상태코드는 201인 POST요청을 제외하고 기본적으로 항상 200이고, 데코레이터를 추가하여 쉽게 동작을 변경할 수 있다.

## Header
```
@Post()
@Header('Cache-Control', 'none')
create() {
  return 'This action adds a new cat';
}
```
- 사용자 정의 응답 헤더를 지정하려면 @Header()데코레이터 또는 라이브러리별 응답 객체를 사용하고 res.header()직접 호출할 수 있습니다.

## Redirection
```
@Get()
@Redirect('https://nestjs.com', 301)
```
- 응답을 특정 URL로 리디렉션하려면 @Redirect()데코레이터 또는 라이브러리별 응답 개체를 사용하고 res.redirect()직접 호출할 수 있습니다.
- @Redirect()두 개의 인수를 취하고 url, statusCode둘 다 선택 사항입니다. 생략하면 기본값 statusCode은 302( )입니다.
```
{
  "url": string,
  "statusCode": number
}
```
- 때로는 HTTP 상태 코드 또는 리디렉션 URL을 동적으로 결정해야 할 수 있습니다. 다음과 같은 모양을 가진 경로 처리기 메서드에서 개체를 반환하여 이 작업을 수행합니다.
```
@Get('docs')
@Redirect('https://docs.nestjs.com', 302)
getDocs(@Query('version') version) {
  if (version && version === '5') {
    return { url: 'https://docs.nestjs.com/v5/' };
  }
}
```
- 반환된 값은 @Redirect()데코레이터에 전달된 모든 인수를 재정의합니다.

## Route parameters
```
@Get(':id')
findOne(@Param() params): string {
  console.log(params.id);
  return `This action returns a #${params.id} cat`;
}
```
- 동적 데이터 를 요청의 일부로 수락해야 하는 경우(예: GET /cats/1cat 을 id로 가져오기 위해 ) 정적 경로가 있는 경로는 작동하지 않습니다 
- 매개변수가 있는 경로를 정의하기 위해 경로의 경로에 경로 매개변수 토큰 을 추가하여 요청 URL의 해당 위치에서 동적 값을 캡처할 수 있습니다. 
- @Get()아래 데코레이터 예제 의 경로 매개변수 토큰은 이 사용법을 보여줍니다. 
- 이러한 방식으로 선언된 경로 매개변수는 @Param()메서드 서명에 추가되어야 하는 데코레이터를 사용하여 액세스할 수 있습니다.
