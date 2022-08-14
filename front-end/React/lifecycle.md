# LifeCycle?
- 컴포넌트가 웹 페이지에 나타났다가 사라지는 과정을 나타냄.

**가상DOM**   
 - 메모리 상에서 돌아가는 가짜 DOM.
 - 기존 DOM과 어떤 행동 후 새로 그린 가상 DOM을 비교해서 바뀐 부분만 갈아 끼워줌. -> 돔 업데이트 처리가 간결함.

![Lifecycle](https://teamsparta.notion.site/image/https%3A%2F%2Fs3-us-west-2.amazonaws.com%2Fsecure.notion-static.com%2F503b6fe9-9af4-4898-8cde-8d29b8085826%2F_2020-10-17__4.26.12.png?table=block&id=3e9d509c-73ce-4f40-9604-0331b02f6d8e&spaceId=83c75a39-3aba-4ba4-a792-7aefe4b07895&width=1800&userId=&cache=v2)   
- 컴포넌트는 생성되고 → 수정(업데이트)되고 → 사라진다.
- 생성은 처음으로 컴포넌트를 불러오는 단계.
- 수정(업데이트)는 사용자의 행동(클릭, 데이터 입력 등)으로 데이터가 바뀌거나, 부모 컴포넌트가 렌더링할 때 업데이트 된다. 아래의 경우에 해당함.
    - props가 바뀔 때
    - state가 바뀔 때
    - 부모 컴포넌트가 업데이트 되었을 때(=리렌더링했을 때)
    - 또는, 강제로 업데이트 했을 경우! (forceUpdate()를 통해 강제로 컴포넌트를 업데이트할 수 있습니다.)
- 제거는 페이지를 이동하거나, 사용자의 행동(삭제 버튼 클릭 등)으로 인해 컴포넌트가 화면에서 사라지는 단계입니다.

# LifeCycle Method
```javascript
import React from "react";

// 클래스형 컴포넌트는 이렇게 생겼습니다!
class LifecycleEx extends React.Component {
  // 생성자 함수
  constructor(props) {
    super(props);

    this.state = {
      cat_name: "나비",
    };

    console.log("in constructor!");
  }

  changeCatName = () => {
    // state를 업데이트하는 방법
    this.setState({cat_name: "바둑이"});

    console.log("고양이 이름을 바꾼다!");
  };

  componentDidMount() {
    // 첫번째 렌더에만 호출됨. API를 가져오거나 등등..
    console.log("in componentDidMount!");
  }

  componentDidUpdate(prevProps, prevState) {
    // 리렌더링이 끝난 다음에 호출됨.
    console.log(prevProps, prevState);
    console.log("in componentDidUpdate!");
  }

  componentWillUnmount() {
    console.log("in componentWillUnmount!");
  }

  render() {
    console.log("in render!");

    return (
      <div>
        {/* render 안에서 컴포넌트의 데이터 state를 참조할 수 있다. */}
        <h1>제 고양이 이름은 {this.state.cat_name}입니다.</h1>
        <button onClick={this.changeCatName}>고양이 이름 바꾸기</button>
      </div>
    );
  }
}

export default LifecycleEx;

```
