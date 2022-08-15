# Redux ?
- Javascript application들의 state(상태)를 관리하는 방법.
- Angular, Vue.js, React, Vanilla Javascript 등 자바스크립트 안에서는 원하는 곳에서 다 쓸 수 있음.
- React에 의존하는 것이 절대 아님!

# Make store 
```javascript
const store = createStore(reducer);
```
- store는 내 state를 넣을 수 있는 장소, create를 통해 장소를 생성할 수 있다.
- state는 application안에서 바뀌는 date를 말한다.

# Reducer
```javascript
// Example
const countModifier = (count = 0, action) => {
  // ... modify context
  switch (action.type) {
    case "ADD":
      return count + 1;
    case "MINUS":
      return count - 1;
    default:
      return count;
  }
};
```
- Reducer는 내 data를 수정(modify)하는 "함수". return 하는 것은 application의 data가 되는 것이다.
- 이 Reducer를 제외한 다른 것들은 state를 함부로 수정할 수 없다.
- if문을 사용해도 되지만 switch가 편함.

# Action
```javascript
const handleAdd = () => {
  countStore.dispatch({ type: ADD });
};
```
- action은 state 변경을 일으키는 이벤트에 대한 정보이다.
- Reducer가 Action과 이전state를 참고하여 새로운 state를 만들기 때문에 Action은 reducer가 구분할 수 있도록 액션의 이름(타입)과 데이터를 가진 객체 형식임.

```javascript
const handleAdd = () => {
  countStore.dispatch({ type: ADD });
};

add.addEventListener("click", handleAdd);
minus.addEventListener("click", () => countStore.dispatch({ type: MINUS }));
```
- action을 보낼 수 있는 방법은 dispatch() 함수를 사용하여 reducer로 메세지를 보낸다.

# Subscribe
```javascript
const onChange = () => {
  number.innerText = countStore.getState();
};

store.subscribe(() => console.log(store.getState()));
```
- subscribe는 state의 변화에 반응한다.
