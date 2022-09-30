# Enum

열거형은 TypeScript가 제공하는 기능 중 하나입니다.   
enum은 열거형으로 이름이 있는 상수들의 집합을 정의할 수 있습니다.   
열거형을 사용하면 의도를 문서화 하거나 구분되는 사례 집합을 더 쉽게 만들수 있습니다. TypeScript는 숫자와 문자열-기반 열거형을 제공합니다.   

숫자 열거형 (Numeric enums)   
```
enum Direction {
Up = 1,
Down,
Left,
Right,
}
```

```
문자열 열거형 (String enums)
enum Direction {
Up = "UP",
Down = "DOWN",
Left = "LEFT",
Right = "RIGHT",
}
```
등등..
