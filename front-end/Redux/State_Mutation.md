# Never Mutate State
- store를 수정할 수 있는 유일한 방법은 action으로 reducer에 메시지를 보내는 것.
- muatation은 예를 들어 array에 push나 pop을 통해 변경시키는 것을 말함.
- state를 수정하려면, 새로운 object나 array를 만들어 return 해야 함.

# Add $ Delete
```javascript
//reducer의 2개의 인자는 state와 action!
const reducer = (state = [], action) => {
  switch (action.type) {
    case ADD_TODO:
      return [{ text: action.text, id: Date.now() }, ...state];
    case DELETE_TODO:
      return state.filter((toDo) => toDo.id !== parseInt(action.id));
    default:
      return state;
  }
};
```
- 위와 같이 ES6의 spread함수나 filter함수를 통해 새로운 배열을 만들어내고 return을 하는 방법을 사용해야 한다.
