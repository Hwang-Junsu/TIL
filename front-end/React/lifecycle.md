# LifeCycle?
- 컴포넌트가 웹 페이지에 나타났다가 사라지는 과정을 나타냄.

**가상DOM**   
 - 메모리 상에서 돌아가는 가짜 DOM.
 - 기존 DOM과 어떤 행동 후 새로 그린 가상 DOM을 비교해서 바뀐 부분만 갈아 끼워줌. -> 돔 업데이트 처리가 간결함.

![Lifecycle](https://kyun2da.dev/static/69e54fe57da139eabae168b5e8304af4/01645/lifecycle.png)   

# 리액트 라이프사이클의 이해

## 리액트 라이프 사이클이란?
리액트는 컴포넌트 기반의 View를 중심으로 한 라이브러리이다. 그러다보니 각각의 컴포넌트에는 라이프사이클 즉, 컴포넌트의 수명 주기가 존재한다.    
컴포넌트의 수명은 보통 페이지에서 렌더링되기 전인 준비 과정에서 시작하여 페이지에서 사라질 때 끝이난다.

## 라이프사이클의 분류
크게 세가지 유형으로 나눌 수 있는데 생성 될때, 업데이트 할 때, 제거할 때이다. 이를 리액트에서는 마운트, 업데이트, 언마운트라고 한다.     
앞으로 위의 그림👆 을 보면서 아래 글을 참조한다면 더욱 더 유용한 글이 될 것 같다. 사실 위 그림이 리액트 사이클의 전부이긴 하다. 😁

여기서 마운트는 DOM이 생성되고 웹 브라우저 상에서 나타나는 것을 뜻하고, 반대로 언마운트는 DOM에서 제거되는 것을 뜻한다.

주의하여 볼 것은 업데이트 부분인데, 업데이트는 다음과 같은 4가지 상황에서 발생한다.

- props가 바뀔 때
- state가 바뀔 때
- 부모 컴포넌트가 리렌더링 될 때
- this.forceUpdate로 강제로 렌더링을 트리거할 때
그럼 이제 본격적으로 각각의 라이프 사이클이 무엇이고 어떻게 Class와 Hooks를 활용한 함수형 컴포넌트에서 사용하는지 알아보도록 하자.🚀

## 라이프 사이클 메서드 살펴보기

1. constructor
자바 같은 언어를 써봤다면 들어봤을 만한 constructor(생성자)이다. 이것은 자바와 마찬가지로 컴포넌트를 만들 때 처음으로 실행된다. 이 메서드에서는 초기 state를 정할 수 있다.
```
// Class
class Example extends React.Component {
    constructor(props) {
        super(props);
        this.state = { count: 0 };
}

// Hooks
const Example = () => {
    const [count,setCount] = useState(0);
}
```
클래스형에서는 초기 state를 정할 때 constructor를 사용해야한다. 하지만 훅에서는 useState hook을 사용하면 초기 상태를 쉽게 설정해줄 수 있다.

2. getDerivedStateFromProps
- 추후 리액트 측에서 업데이트 할 시 보충 필요

이 메서드는 리액트 16.3버전 이후에 생긴 메서드이다. props로 받아 온 값을 state에 동기화시키는 용도로 사용하며, 컴포넌트가 마운트될 때와 업데이트 될 때 호출된다.

나는 아직 이 메서드를 써본적이 없긴한데 다음의 예같은 곳에서 쓰인다고 한다. 아직 써본적이 없어서 class에서의 메서드 사용법과 hooks 사용 예를 간단히 링크로 남겨놓고 쓰게 된다면 포스팅을 수정하도록 해야겠다.
```
// Class
class Example extends React.Component {
  static getDerivedStateFromProps(nextProps, prevState) {
    if (nextProps.value !== prevState.value) {
      return { value: nextProps.value }
    }
    return null
  }
}
```
3. shouldComponentUpdate
이 메서드는 props나 state를 변경했을 때, 리렌더링을 할지 말지 결정하는 메서드이다. 이 메서드에서는 반드시 true나 false를 반환해야한다. 이 메서드는 오직 성능 최적화만을 위한 것이며 렌더링 목적을 방지하는 목적으로 사용하게된다면 버그로 이어질 수 있다.
```
// Class
class Example extends React.Component {
  shouldComponentUpdate(nextProps) {
    return nextProps.value !== this.props.value
  }
}

// Hooks
const Example = React.memo(() => {
      ...
  },
  (prevProps, nextProps) => {
    return nextProps.value === prevProps.value
  }
)
```
클래스형도 보통은 PureComponent를 추천한다고 하고 Hooks 에서도 props는 React.memo, state는 useMemo를 활용하면 렌더링 성능을 개선할 수 있다고 한다.    

4. render
이는 가장 기초적인 메서드이기도하고 가장 중요한 메서드이기도 하다. 컴포넌트를 렌더링할 때 필요한 메서드로 유일한 필수 메서드이기도 하다. 함수형 컴포넌트에서는 render를 안쓰고 컴포넌트를 렌더링할 수 있다.
```
// Class
class Example extends React.Component {
  render() {
    return <div>컴포넌트</div>
  }
}

// Hooks
const example = () => {
  return <div>컴포넌트</div>
}
```
5. getSnapshotBeforeUpdate
- 추후 리액트 측에서 업데이트 할 시 보충 필요

이 메서드는 render에서 만들어진 결과가 브라우저에 실제로 반영되기 직전에 호출된다. 공식문서의 말을 따보자면 이 메서드에 대한 사용 예는 흔하지 않지만, 채팅 화면처럼 스크롤 위치를 따로 처리하는 작업이 필요한 UI 등을 생각해볼 수 있다고한다.
```
class Example extends React.Component {
  getSnapshotBeforeUpdate(prevProps, prevState) {
    if (prevProps.list.length < this.props.list.length) {
      const list = this.listRef.current
      return list.scrollHeight - list.scrollTop
    }
    return null
  }
}
```
함수형에서는 아직 이 기능을 대체할만한 hook이 없다고 한다..


6. componentDidMount
이 메서드는 컴포넌트를 만들고 첫 렌더링을 마친 후 실행한다. 함수형 Hooks 에서는 useEffect를 활용하여 다음의 기능을 구현할 수 있다.
```
// Class
class Example extends React.Component {
    componentDidMount() {
        ...
    }
}

// Hooks
const Example = () => {
    useEffect(() => {
        ...
    }, []);
}
```
여기서 useEffect의 [] 의존성 배열을 비워야지만 똑같은 메소드를 구현할 수 있다.

useEffect에 익숙하지 않으신 분들이라면 리액트 공식문서-useEffect를 참조하면 좋을 것 같다.

7. ComponentDidUpdate
이것은 리렌더링을 완료한 후 실행한다. 업데이트가 끝난 직후이므로, DOM관련 처리를 해도 무방하다.
```
// Class
class Example extends React.Component {
    componentDidUpdate(prevProps, prevState) {
        ...
    }
}

// Hooks
const Example = () => {
    useEffect(() => {
        ...
    });
}
```
8. componentWillUnmount
이 메서드는 컴포넌트를 DOM에서 제거할 때 실행한다. componentDidMount에서 등록한 이벤트가 있다면 여기서 제거 작업을 해야한다. 함수형 컴포넌트에서는 useEffect CleanUp 함수를 통해 해당 메서드를 구현할 수 있다.
```
// Class
class Example extends React.Component {
    coomponentWillUnmount() {
        ...
    }
}

// Hooks
const Example = () => {
    useEffect(() => {
        return () => {
            ...
        }
    }, []);
}
```
9. componentDidCatch
- 추후 리액트 측에서 업데이트 할 시 보충 필요

마지막으로 맨 위의 사진에는 보이지 않지만 componentDidCatch라는 메서드가 존재한다. 이 메서드는 컴포넌트 렌더링 도중에 에러가 발생 했을 때 애플리케이션이 멈추지 않고 오류 UI를 보여줄 수 있게 해준다.
```
// Class
class Example extends React.Component {
  componentDidCatch(error, info) {
    console.log('에러가 발생했습니다.')
  }
}
```
리액트 공식문서에서는 곧 Hooks에 해당 라이프 사이클 메서드를 추가할 예정이 있다고 한다.

## 마치며
이렇게 리액트의 모든 라이프사이클에 대해 알아보았다. 최근 클래스형보다는 Hooks를 활용한 함수형 컴포넌트가 많이 쓰이고 있는 만큼 리액트 Hooks를 활용하여 라이프 사이클을 구현하는 것이 실무에서는 핵심이 된 것 같다. 앞으로 바뀐 부분이 있거나 추가된 부분이 있다면 그때마다 와서 수정을 하도록 해야겠다.
