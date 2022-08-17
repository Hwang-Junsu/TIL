# install styled-component
- 패키지 설치하기
```bash
yarn add styled-components
```

# style-component?
- CSS-in-JS 라이브러리 중 하나. 컴포넌트에 스타일을 직접 입히는 방식.
- 장점은 class 이름짓기에 자유로워지고, 컴포넌트에 스타일을 적기 때문에, 간단하고 직관적임.
- 각각의 컴포넌트에 랜덤하게 class이름이 적용된다.

# Use
```javascript
const Box = styled.div`
  background-color: ${(props) => props.bgColor};
  width: 100px;
  height: 100px;
`;

<Box bgColor="teal" />
```

- styled 뒤에 "."을 찍고 html태그를 설정한다. 백틱(``)안에 css 내용을 작성해주면 기본적인 틀 완성.
- 컴포넌트의 props를 설정해 주어서 변수를 통한 속성변경이 가능하다.

```javascript
const Circle = styled(Box)`
  border-radius: 50px;
`;
```
- styled(컴포넌트) 형식으로 컴포넌트의 모든 속성을 상속받고, 일부만 변경해줄 수 있다.


# styled-component 
https://styled-components.com/docs
