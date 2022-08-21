# React Hook ?

- React에서 기존에 사용하던 Class를 이용한 코드를 작성할 필요 없이, state와, 여러 React 기능을 사용할 수 있도록 만든 라이브러리
- React 16.8 버전(2019년도)에 추가된 공식 라이브러리
- 현재 공식문서에서는, Class형 컴포넌트보다는 Function형 component로 새로운 React 프로젝트를 만들기를 권장.

# Hook 규칙

1. 최상위에서만 Hook을 호출.
2. React 함수에서만 Hook을 호출
3. Hook을 만들 때 앞에 use를 붙인다.
4. React는 Hook에 노출되는 순서에 의존한다.


# useState

- useState는 컴포넌트에서 state값을 추가할 때 사용된다.

1. import
```javascript
import {useState} from "react";
```

2. useState 선언
```javascript
const [count, setCount] = useState(0)
```
- useState() 호출 시 배열을 반환하는데, 첫 번째 원소는 상태값, 두 번째 원소는 상태를 업데이트 해주는 함수임.
- 이 함수에 파라미터를 넣어서 호출하게 되면 전달받은 파라미터로 값이 바뀌고 컴포넌트는 리렌더링 된다.
- 호출 부분() 에 초기 설정 값을 넣을 수 있다. 

# useEffect
- 화면 렌더링이 될 때마다 state 값을 내가 필요한 데이터 모양새로 바꿔 업데이트 할 때 사용된다.

1.import
```javascript
import {useEffect} from "react";
```

2. useEffect 선언
```javascript
useEffect(() => {
    document.title = '업데이트 횟수: ${count}';
}, []);
```
- 매개변수로 익명함수와 빈 배열 두가지가 들어간다.
- 두 번째 매개변수인 배열에 빈 배열을 넣으면 화면에 처음 렌더링 될 때 한번 만 실행된다. 값을 넣게 되면, 그 값의 상태가 업데이트 될 때만 실행이된다.
- 생략한다면 리랜더링할때마다 반복실행된다.

# useRef
- 자바스크립트에서는 특정 DOM(태그)를 선택할 때 Dom selector 함수((getElementById ...)를 사용하지만 리액트에서는 useRef를 사용한다.

1. import
```javascript
import {useRef} from "react"
```

2. useRef 선언
```javascript
const nameRef = useRef(null);

nameRef.current.focus();
```
- 초기값으로 null을 넣어주었음.
- 원하는 위치의 component에 ref={} 를 집어 넣어준다.
- 포커스를 잡을 때 nameRef.current.focus() 형태로 작성한다.
