# Recoil
React를 위한 상태관리 라이브러리
```npm install recoil```

## RecoilRoot
recoil 상태를 사용하는 컴포넌트는 부모 트리 어딘가에 나타나는 RecoilRoot 가 필요하다. Root 컴포넌트가 RecoilRoot를 넣기에 가장 좋은 장소다.

## Atom
Atom은 상태(state)의 일부를 나타낸다. Atoms는 어떤 컴포넌트에서나 읽고 쓸 수 있다.   
atom의 값을 읽는 컴포넌트들은 암묵적으로 atom을 구독한다.   
그래서 atom에 어떤 변화가 있으면 그 atom을 구독하는 모든 컴포넌트들이 리렌더링 되는 결과가 발생할 것이다.   
atom(): 쓰기 가능한 state를 나타내는 atom를 만듭니다.   
```
const textState = atom({
key: 'textState', // 유니크한 ID(다른 atom/selector와 관련하여)
default: '', // 기본값 (초기값)
});
```

## useRecoilState()
컴포넌트가 atom을 읽고 쓰게 하기 위해서는 useRecoilState()를 아래와 같이 사용하면 된다.   
ex) const [text, setText] = useRecoilState(textState);   

https://recoiljs.org/ko/docs/introduction/getting-started

## useRecoilValue(state)

Recoil state값을 반환합니다.
이 hook은 암묵적으로 주어진 상태에 컴포넌트를 구독합니다.
이 hook는 읽기 전용 상태와 쓰기 가능 상태에서 모두 동작하므로 컴포넌트가 상태를 읽을 수만 있게 하고 싶을 때에 추천하는 hook입니다. 이 hook을 React 컴포넌트에서 사용하면 상태가 업데이트 될 때 리렌더링을 하도록 컴포넌트를 구독합니다.
ex) const names = useRecoilValue(namesState);

https://recoiljs.org/ko/docs/api-reference/core/useRecoilValue/

## useSetRecoilState(state)

Recoil state의 값을 업데이트하기 위한 setter 함수를 반환합니다.
상태를 변경하기 위해 비동기로 사용될 수 있는 setter 함수를 리턴합니다.
setter는 새로운 값이나 이전 값을 인수로 받는 updater 함수를 넘겨줍니다.
ex) const setNamesState = useSetRecoilState(namesState);

https://recoiljs.org/ko/docs/api-reference/core/useSetRecoilState/
