# Provider
- 공급자는 Nest의 기본 개념입니다. 기본 Nest 클래스의 대부분은 서비스, 리포지토리, 팩토리, 도우미 등 공급자로 취급될 수 있습니다. 
- 공급자의 주요 아이디어 는 종속성 으로 주입 될 수 있다는 것입니다
- 즉, 개체는 서로 다양한 관계를 생성할 수 있으며 개체의 인스턴스를 "연결"하는 기능은 대부분 Nest 런타임 시스템에 위임될 수 있습니다.

# 의존성 주입
Nest에서는 TypeScript 기능 덕분에 유형별로 해결되기 때문에 종속성을 관리하기가 매우 쉽습니다.     
아래 예에서 Nest는 catsService의 인스턴스를 생성하고 반환하여 해결합니다 CatsService(또는 싱글톤의 일반적인 경우 다른 곳에서 이미 요청된 경우 기존 인스턴스를 반환).    
이 종속성은 해결되어 컨트롤러의 생성자로 전달됩니다(또는 표시된 속성에 할당됨).    
```
constructor(private catsService: CatsService) {}
```

# Provider register
```
import { Module } from '@nestjs/common';
import { CatsController } from './cats/cats.controller';
import { CatsService } from './cats/cats.service';

@Module({
  controllers: [CatsController],
  providers: [CatsService],
})
export class AppModule {}
```
- 이제 공급자( CatsService)를 정의하고 해당 서비스( )의 소비자가 CatsController있으므로 주입을 수행할 수 있도록 Nest에 서비스를 등록해야 합니다.
- 모듈 파일( )을 편집하고 데코레이터 의 배열에 app.module.ts서비스를 추가하여 이를 수행합니다 .providers@Module()
