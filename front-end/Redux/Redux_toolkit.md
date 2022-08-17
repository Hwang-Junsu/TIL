# 기존 Redux
```javascript
const ADD = "ADD";
const DELETE = "DELETE";

export const addToDo = (text) => {
  return {
    type: ADD,
    text,
  };
};

export const deleteToDo = (id) => {
  return {
    type: DELETE,
    id,
  };
};

const reducer = (state = [], action) => {
  switch (action.type) {
    case ADD:
      return [{ text: action.text, id: Date.now() }, ...state];
    case DELETE:
      return state.filter((toDo) => toDo !== action.id);
    default:
      return state;
  }
};

export const actionCreators = {
  addToDo,
  deleteToDo,
};
```
- 기존의 Redux에서는 {type: "ADD", id: Date.now()} 와 같은 딕셔너리 형식으로 action을 만들어 dispatch해주어 reducer를 작동시키는 방식.
- 복잡한 방식으로 Redux 공식 문서에서 새로운 방식을 제안했다.

# Redux - createAction, createReducer
```javascript
const addToDo = createAction("ADD");
const deleteToDo = createAction("DELETE");
const reducer = createReducer([], {
   [addToDo]: (state, action) => {
     state.push({ text: action.payload, id: Date.now() });
   },
   [deleteToDo]: (state, action) =>
     state.filter((toDo) => toDo.id !== action.payload),
});
```
- createAction을 통해 action을 만들어주고, state와 payload를 포함한 객체를 반환시켜 준다.

# Redux - createSlice
```javascript
const toDos = createSlice({
  name: "toDosReducer",
  initialState: [],
  reducers: {
    add: (state, action) => {
      state.push({ text: action.payload, id: Date.now() });
    },
    remove: (state, action) =>
      state.filter((toDo) => toDo.id !== action.payload),
  },
});
```
- 더 나아가 createSlice를 통해 더 간단하게 state와 reducer를 짧은 코드로 생성하고 관리할 수 있는 기능을 제공한다.
- toDos의 console을 찍게되면 reducers 함수들을 포함하고 있어, 사용에도 용이하다.


# configureStore
```javascript
const store = configureStore({ reducer: toDos.reducer });
```
- createStore보다 더 나은 개발(번거로운 기본 설정들을 자동으로 해줌)을 위해 저장소 설정에 default를 추가할 수 있음.
- configureStore함수는 reducer, middleware, devTools, preloadedState, enchancer가 전달된다.






































