# Module
- @Module()모듈은 데코레이터 로 주석이 달린 클래스 입니다. 데코레이터는 Nest 가 애플리케이션 구조를 구성하는 데 사용하는 메타 @Module()데이터를 제공합니다 .
- 모듈 은 기본적으로 공급자를 캡슐화 합니다. 즉, 현재 모듈의 일부도 아니고 가져온 모듈에서 내보낸 것도 아닌 공급자를 주입할 수 없습니다. 
- 따라서 모듈에서 내보낸 공급자를 모듈의 공용 인터페이스 또는 API로 간주할 수 있습니다.

### 데코레이터 속성
- providers	: Nest 인젝터에 의해 인스턴스화되고 적어도 이 모듈에서 공유될 수 있는 제공자
- controllers	: 인스턴스화해야 하는 이 모듈에 정의된 컨트롤러 세트
- imports	: 이 모듈에 필요한 공급자를 내보내는 가져온 모듈 목록
- exports	: 그 하위 집합은 providers이 모듈에서 제공하며 이 모듈을 가져오는 다른 모듈에서 사용할 수 있어야 합니다. 공급자 자체 또는 해당 토큰( provide값) 만 사용할 수 있습니다.
# Feature modules
```
import { Module } from '@nestjs/common';
import { CatsController } from './cats.controller';
import { CatsService } from './cats.service';

@Module({
  controllers: [CatsController],
  providers: [CatsService],
})
export class CatsModule {}
```
-  기능 모듈은 단순히 특정 기능과 관련된 코드를 구성하여 코드를 구성하고 명확한 경계를 설정합니다. 
-  이는 특히 애플리케이션 및/또는 팀의 규모가 커짐에 따라 복잡성을 관리하고 SOLID 원칙으로 개발하는 데 도움이 됩니다
