# Typescript vs Javascript
- Typescript는 Javascript의 확장판.
- JS는 코드 실행 전 타입에 대한 정의가 존재하지 않는다. TS는 언어 자체에게 그 값들이 어떤 것인지, 타입들이 어떤 것인 지 말해준다.
- 타입을 설명해 줌으로써, 실수를 방지하고, 정보를 보호할 수 있다.

# Typescript
```typescript
const plus(a:number, b:number) => a+b
```
- column(:)을 통해 type을 지정해준다. 위 예시는 a와 b가 항상 number형이라는 것을 명시.
- 우리는 component의 prop들에 타입을 지정하는 법을 알아야 함.

# interface
```typescript
interface DummyProps {
  text: string;
  active?: boolean;
}

function Dummy({text, active = false} : DummyProps) {
  return <H1>{text}</H1>
}

return (<Dummy text="blahblah"/>)
```
- 타입스크립트에게 오브젝트 내의 데이터를 설명해주기 위해 interface를 생성한다.
- optional(require가 아닌 선택적으로 변수를 사용하게 하는 방법)하게 사용하기 위해서는 interface 해당 변수 앞에 물음표(?)를 붙인다.
- component의 매개변수 안에 "="를 사용하여 prop에 default를 설정해 줄 수 있다.


# event
```typescript
const onClick = (event:React.FormEvent<HTMLButtonElement>) => {

}

return (
  <form>
    <button onClick={onClick}> click me </button>
  </form>
)
```
- Form 내부에 있다면 event:React.FormEvent<HTMLButtonElement>라고 명시, button만 있다면 React.MouseEvent<HTMLButtonElement> 라는 식으로 타입을 명시해야한다.
- 이런식으로 event를 특정짓는 것은 모든 패키지에서 동일하게 사용되지는 않는다. (React.js에서만 이렇게 사용)
  
  

# SyntheticEvent
- ReactJS는 자바스크립트의 실제 이벤트를 넘겨주는게 아님. SyntheticEvent를 주는 것.
- ReactJS가 최적화한 이벤트들을 SyntheticEvent라고 부름.
- [SyntheticEvent Doc](https://reactjs.org/docs/events.html)
