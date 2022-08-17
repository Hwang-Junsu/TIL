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

```javascript
const Father = styled.div`
  display: flex;
`;

const Btn = styled.button`
  color: white;
  background-color: tomato;
  border: 0;
  border-radius: 15px;
`;

const Link = styled(Btn)``;

const Input = styled.input.attrs({ required: true, minLength: 10 })`
  background-color: tomato;
`;

function App() {
  return (
    <Father as="header">
      <Input />
      <Input />
      <Input />
    </Father>
  );
}
```
- as 속성을 이용해 html 태그 속성을 바꿔줄 수 있다.
- styled.tag.attrs({property: value})를 통해서 필요한 속성들을 지정해 줄 수 있다.


# Animation
```javascript
import styled, { keyframes } from "styled-components";

const Wrapper = styled.div`
  display: flex;
`;

const rotationAnimation = keyframes`
0%{
  transform:rotate(0deg);
  border-radius: 0px;
}
50% {
  border-radius: 100px;
}
100% {
  transform:rotate(360deg);
  border-radius: 0px;
}
`;

const Box = styled.div`
  height: 200px;
  width: 200px;
  background-color: tomato;
  display: flex;
  justify-content: center;
  align-items: center;
  animation: ${rotationAnimation} 1s linear infinite;
`;
```
- keyframs를 import해주면, css에서 사용하던 것처럼 똑같이 애니메이션을 사용할 수 있다.

# Pseudo Selector
```javascript
const Box = styled.div`
  height: 200px;
  width: 200px;
  background-color: tomato;
  display: flex;
  justify-content: center;
  align-items: center;
  animation: ${rotationAnimation} 1s linear infinite;

  span {
    font-size: 36px;
    &:hover {
      font-size: 60px;
    }
  }
`;
```
- component 내부의 태그 속성에 대해 css를 부여할 수 있다.
- &를 사용하여 자기자신을 참조할 수 있다.
- 

# styled-component DOC 
https://styled-components.com/docs
