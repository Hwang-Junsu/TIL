# Pipe
- 파이프는 인터페이스 @Injectable()를 구현하는 데코레이터로 주석이 달린 클래스 입니다.PipeTransform
![img](https://docs.nestjs.com/assets/Pipe_1.png)

파이프에는 두 가지 일반적인 사용 사례가 있습니다.    

- 변환 : 입력 데이터를 원하는 형식으로 변환(예: 문자열에서 정수로)
- validation : 입력 데이터를 평가하고 유효한 경우 변경되지 않은 상태로 전달합니다. 그렇지 않으면 데이터가 올바르지 않을 때 예외를 던집니다.

# Pipe
내장 파이프 #
Nest는 즉시 사용할 수 있는 9개의 파이프와 함께 제공됩니다.

- ValidationPipe
- ParseIntPipe
- ParseFloatPipe
- ParseBoolPipe
- ParseArrayPipe
- ParseUUIDPipe
- ParseEnumPipe
- DefaultValuePipe
- ParseFilePipe
@nestjs/common패키지 에서 내 보냅니다.

# Binding pipe
```
@Get(':id')
async findOne(@Param('id', ParseIntPipe) id: number) {
  return this.catsService.findOne(id);
}
```

# Custom Pipe
```
import { PipeTransform, Injectable, ArgumentMetadata } from '@nestjs/common';

@Injectable()
export class ValidationPipe implements PipeTransform {
  transform(value: any, metadata: ArgumentMetadata) {
    return value;
  }
}
```
