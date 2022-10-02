# Get Start
```
$ npm i -g @nestjs/cli // 전역으로 설치
$ nest new project-name // 만들 프로젝트 이름.
```

# Decorator
```
@Injectable()
export class AppService {
  getHello(): string {
    return 'Hello World!';
  }
}
```
- 재사용성을 강화하기 위하여 사용하는 패턴,
- 타입 스크립트의 데코레이터는 파이썬의 데코레이터나 자바의 어노테이션과 유사한 기능을 합니다. 클래스, 메서드, 접근자, 프로퍼티, 매개변수에 적용 가능합니다. 
- 각 요소의 선언부 앞에 @로 시작하는 데코레이터를 선언하면 데코레이터로 구현된 코드를 함께 실행합니다.

# Controllers
앞서 보았듯이, NestJS 어플리케이션은 main.ts에서 시작하고,
이곳에 명시되어있는 하나의 모듈에서 어플리케이션을 생성한다.

app.module은 모든 것의 루트 모듈 역할을 한다.

### @Module이란?

-part of the application.
-module could be .. like an app in dJango!
-dJango에서 하나의 앱이 하나의 기능을 담당했던 것처럼, NestJS에서는 모듈이 그 역할을 대신한다.
-controllers가 하는 일

👉🏻 url 가져오고(url로의 요청을 받음), 함수로 매핑하여, 함수를 실행하는 것 (express의 router같은 역할)    
👉🏻 데코레이터 덕분에 해당 경로로 접속하면 해당 함수를 호출하게 됨    
👉🏻 String 타입을 리턴하고, "Hello everyone"이라는 문구를 리턴한다는 뜻    

# Services
controller는 url을 가져오고 함수를 실행하는 역할을 할 뿐, 실제 비즈니스 로직은 service 내부에 작성한다.   
service 내부에 들어가면 실제 작업을 수행하는 함수를 볼 수 있다.   


이렇게 로직을 service 내부에 작성하고, controller의 리턴 부분에 this.appService.메서드명()을 입력해주면
해당 로직을 수행하도록 리턴하는 것!
