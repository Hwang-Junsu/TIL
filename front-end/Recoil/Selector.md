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
