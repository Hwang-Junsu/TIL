# react-beautiful-dnd
## React로 list를 만들기 위한 아름답고 접근 가능한 드래그 앤 드롭
```
npm i react-beautiful-dnd
npm i --save-dev @types/react-beautiful-dnd
```

https://www.npmjs.com/package/react-beautiful-dnd   
https://github.com/atlassian/react-beautiful-dnd/blob/master/docs/about/installation.md   

react-beautiful-dnd 테스트해 보기
https://react-beautiful-dnd.netlify.app/iframe.html?id=board--simple

react-beautiful-dnd 예시 코드
https://codesandbox.io/s/k260nyxq9v

DragDropContext
https://github.com/LeeHyungGeun/react-beautiful-dnd-kr

## Using innerRef
(Draggable과 Droppable컴포넌트의 내부 props정의)   
< Draggable /> 및 < Droppable /> 컴포넌트 모두 HTMLElement를 제공해야 합니다. 이것은 DraggableProvided 및 DroppableProvided 객체의 innerRef 속성을 사용하여 수행됩니다.   
https://github.com/atlassian/react-beautiful-dnd/blob/master/docs/guides/using-inner-ref.md#using-innerref

## dragHandleProps
특정 영역을 통해서만 드래그를 가능하도록 하고 싶을 때 사용한다.   
ex) {...provided.dragHandleProps}   

DragDropContext   
https://github.com/atlassian/react-beautiful-dnd/blob/HEAD/docs/api/drag-drop-context.md

Droppable   
https://github.com/atlassian/react-beautiful-dnd/blob/HEAD/docs/api/droppable.md

Draggable   
https://github.com/atlassian/react-beautiful-dnd/blob/HEAD/docs/api/draggable.md

## onDragEnd
- result: DropResult
- result.draggableId: 드래그 되었던 Draggable의 id.
- result.type: 드래그 되었던 Draggable의 type.
- result.source: Draggable 이 시작된 위치(location).
- result.destination: Draggable이 끝난 위치(location). 만약에 Draggable이 시작한 위치와 같은 위치로 돌아오면 이 destination값은 null이 될것입니다.

## Array.prototype.splice()
array.splice(start[, deleteCount[, item1[, item2[, ...]]]])   
splice() 메서드는 배열의 기존 요소를 삭제 또는 교체하거나 새 요소를 추가하여 배열의 내용을 변경합니다.   
```
const months = ['Jan', 'March', 'April', 'June'];
months.splice(1, 0, 'Feb');
console.log(months); // expected output: Array ["Jan", "Feb", "March", "April", "June"]
```
https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/Array/splice

## < Draggable /> list의 키
< Draggable /> list를 렌더링하는 경우 각 < Draggable />에 key prop을 추가하는 것이 중요합니다.

- 규칙
1. key는 list 내에서 고유해야 합니다.
2. key에 item의 index가 포함되어서는 안 됩니다. (map의 index사용 X)
3. 일반적으로 draggableId를 key로 사용하면 됩니다.
주의! list에 key가 없으면 React가 경고하지만 index를 key로 사용하는 경우 경고하지 않습니다.   
key를 올바르게 사용하지 않으면 정말 안 좋은 일이 생길 수 있습니다 💥   
```
return items.map((item, index) => (
< Draggable
// adding a key is important!
key={item.id}
draggableId={item.id}
index={index}
>
나머지 코드..
```
https://github.com/atlassian/react-beautiful-dnd/blob/HEAD/docs/api/draggable.md#keys-for-a-list-of-draggable-

+ Card를 드래그한 후 이동하지 않고, 다시 제자리에 놓았을 때, 콘솔창에 에러 발생하시는 분들은 destination?.index가 undefined일 때 return으로 함수를 종료시켜주시면 됩니다.
```
if (destination?.index === undefined) return;
```
