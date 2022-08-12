# HTML
- Hypertext Markup Language는 마크업 언어.   
`마크업은 이름 그대로 표시하는 것. 이미지가 들어가는 곳, 글이 들어가는 곳`  

# Example
```HTML
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta http-equiv="X-UA-Compatible" content="IE=edge" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>오늘의 투두</title>
  </head>
  <body>
    <h1>오늘 할 일</h1>
    <div>
      <h3>고양이 밥주기</h3>
      <p>고양이 물, 사료 챙겨주기</p>
      <button>완료</button>
    </div>
    <div>
      <h3>장보기</h3>
      <p>토마토, 계란, 초코렛 사기</p>
      <button>완료</button>
    </div>
    <div>
      <h3>코딩하기</h3>
      <p>리액트 강의 1주차 듣기</p>
      <button>완료</button>
    </div>
  </body>
</html>

```
- <, > (꺽새)모양을 태그라고 부르고, 그 안의 div, button 등을 요소라고 부른다.


# DOM(문서 객체 모델)
- DOM은 html 단위 하나하나를 객체로 생각하는 모델. 예를 들면, 'div'라는 객체는 텍스트 노드, 자식 노드 등 하위의 어떤 값을 가지고 있다. 이런 구조를 트리 구조라고 한다.
- 즉, DOM은 트리구조.
- console창에서 children, childNode, getElementsByTagName 등 자식요소에 접근할 수 있음.
