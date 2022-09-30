# Selectors

Selector는 파생된 state(derived state)의 일부를 나타낸다.   
즉, 기존 state를 가져와서, 기존 state를 이용해 새로운 state를 만들어서 반환할 수 있다.    
기존 state를 이용만할 뿐 변형시키지 않는다. derived state는 다른 데이터에 의존하는 동적인 데이터를 만들 수 있기 때문에 강력한 개념이다.   
```
const filteredTodoListState = selector({
key: 'filteredTodoListState',
get: ({get}) => {
const filter = get(todoListFilterState);
const list = get(todoListState);

switch (filter) {
case 'Show Completed':
return list.filter((item) => item.isComplete);
case 'Show Uncompleted':
return list.filter((item) => !item.isComplete);
default:
return list;
}
},
});
```
filteredTodoListState는 내부적으로 2개의 의존성 todoListFilterState와 todoListState을 추적한다. 그래서 둘 중 하나라도 변하면 filteredTodoListState는 재 실행된다.
   
https://recoiljs.org/ko/docs/basic-tutorial/selectors/
https://recoiljs.org/ko/docs/api-reference/core/selector/

## set? 
- 이 속성이 설정되면 selector는 쓰기 가능한 상태를 반환한다. 첫번째 매개변수로 콜백 객체와 새로 입력 값이 전달된다. 
- 사용자가 selector를 재설정할 경우 새로 입력 값은 T 타입의 값 또는 DefaultValue 타입의 객체일 수 있다. 콜백에는 다음이 포함된다.

### get 매개변수
다른 atom이나 selector로부터 값을 찾는데 사용되는 함수. 이 함수는 selector를 주어진 atom이나 selector를 구독하지 않는다.

### set 매개변수
업스트림 Recoil 상태의 값을 설정할 때 사용되는 함수. 첫 번째 매개변수는 Recoil state, 두 번째 매개변수는 새로운 값(newValue)이다. 새로운 값은 업데이트 함수나 재설정 액션을 전파하는 DefalutValue 객체일 수 있다.
```
const proxySelector = selector({
key: 'ProxySelector',
get: ({get}) => ({...get(myAtom), extraField: 'hi'}),
set: ({set}, newValue) => set(myAtom, newValue),
});
```
https://recoiljs.org/ko/docs/api-reference/core/selector/
