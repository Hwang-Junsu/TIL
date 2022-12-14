# Web ?
- 정보를 전달하기 위함.
- 컨텐츠의 종류에 따라 정보 표현 방식의 차이 발생.

## 표현 방식을 나누는 기준
- 고객이 기준이 된다. (우리는 웹을 무상제공하지 않아요.,,)
- 고객들은 이미 무수한 웹사이트를 이용해본 경험이 있다. 고객은 다 알고 있다. ("사이트가 불편하네.. 이상하네..")
- 사회와 사이트 이용방법에 대한 합의를 본 것. => 즉, 고객이 이용하는 방법에 따라가야 한다.


## 최소한 불편하지 않게 만들기.
- 사용자를 화나게 하지말자.
- 익숙한 사용법이 아닐 때 (팝업 다시보지 않기, 페이지를 넘겼을 때 위로 올라가지 않을 때)
- 원하는 정보를 빠르게 얻지 못할 때. (원하는 정보를 찾기 위해 무수한 페이지를 넘겨야하거나 찾아야 할 때)
- 같은 액션을 여러번 반복할 때.

## 불편하지 않으려면?
- 당연한 걸 하고 당연하지 않은 걸 하지말자. (가장 1순위)
- 사이트 목적에 맞게 필요한 것만 보여주자.(화면을 설계하고 군더더기 없이 배치, 유저가 납득할 수 있게)

## 시선을 생각하자.

- 보통 1번이 편했다고 이야기 한다고 함. 이전 앞에 슬라이드들이 1번이었기 때문.(경로 의존성, 과거의 하나의 선택이 습관 때문에 쉽게 변화되지 않는 현상(ex)쿼티 자판)
- 보편적으로 가장 편하게 느끼는건 4번.
- 시선은 좌-우, 위-아래로 움직인다.
- 정보를 보고 이미지를 보는 것이 좋다.
- 집중할 내용에 시선이 가장 먼저 닿도록! 반복되어 읽히나 매번 읽을 필요없는 정보를 위로 빼고 가장 중요한 내용에 집중하도록 한다.

---
## 최소한의 화면설계 (💡프론트 작업 전 반드시 해야하는 것들)
### 주제를 확실히, 그리고 작게 잡기.
- 운동, 예를 들어 "테니스"는 너무 큰 주제임. "실내 테니스장 찾기" 처럼 주제를 확실히, 작게 잡아야함.
### 주제에 맞는 컨텐츠가 아니라면 전부 빼야한다.
- "실내 테니스장 찾기" 주제라면 배드민턴장 찾기를 벗어난 컨텐츠이다.
### 나와야 할 페이지 정리하기
- 나와야하는 페이지를 전부 적어보기.(아주 상세하게)
- 포스트 잇 한 장 당 한페이지씩, 그 다음 그 페이지에 들어갈 기능을 적어보자.
### 페이지간의 연결 지점을 찾기
- 페이지가 모두 나왔다면 순서를 이어보자, 이어지지 않는 페이지는 필요없거나, 중간과정이 빠진 페이지이다.
- 다른곳으로 이어진 후 다시 돌아와야 한다면, 달라진 점이 있는지 확인하고, 달라진게 있다면 새로운 포스트 잇에 적어주자.
### 포스트잇을 정리해서 문서화
- 모든 화면 흐름과 대략의 기능과 어떤 데이터가 포함되어야 하는 지 명확해진다.
- 이 정리본을 스토리보드라고 한다.
### 집중해서 보여줄 내용을 다 체크.
- 보여줄 데이터가 유저가 보려면 어디에서 페이지 이동을 해야하는 지,
- 맨 위에는 어떤 텍스트 혹은 아이콘이 있어야 하는 지,
- 위 사항을 생각해보고 스토리보드에 추가해보자.
- 모든 기능이 메인페이지에 있을 수 없으니까, 어디에 어느 기능이 있는지 알 수 있도록 툴팁, 스낵바 등 온갖 수단을 동원해서 말을 걸어보자.
- 이 버튼을 누르면 어떤 일이 일어날 지 등도 미리 알려주면 좋다.
- 최대한 유저에게 친절하세요.

---
## 표현과 적응
- 사람은 모두 적응한다. 고객이라고 다를 것이 없음.
### 웹은 기본적으로 단방향 소통
### 유저의 적응을 돕는 길잡이가 필요하다. (툴팁, 스낵바)
- 이러한 길잡이를 인터렉션이라고 한다.

---
## 인터렉션 (사이트를 탐험하는 고객님들을 위한 가이드)
- 인터렉션은 유저와의 소통이다. 사용자의 행동에 맞게 일어나야하고 규칙대로 수행되엉야 함. 그래야 유저가 사이트 사용에 적응할 수 있다.
### 인터렉션의 동작 방식
1. 사용자의 행동을 유도하고,
2. 사용자의 행동이 일어나고,
3. 미리 정한 규칙대로 웹이 반응(피드백) 하고,
4. 다시금 사용자의 행동을 유도해야 한다.
### 도날드 노먼의 인터렉션 원칙
1. 가시성 : 그 기능이 사용자 눈에 띄어야 함.
2. 피드백 : 사용자의 행위 후 일어난 변화를 적절하게 피드백해야 한다.
3. 제한요소 : 특정 상황에서 사용자가 해도 되는 것, 해선 안되는 것을 명확히 규정하고 제한.
4. 맵핑 : 사용자가 특별한 설명이나 도움없이 대상의 기능을 쉽게 떠올리고 이용 가능. (ex 좋아요 👍, 취소 ❌)
5. 일관성 : 적용된 디자인은 일정한 패턴이나 예측가능한 일관성을 지녀야 함. ⭐⭐⭐
6. 행동유도성 : 사용자에게 기대하는 행위가 인지, 유도 되어야 함. (ex 게시글 작성 버튼 ➕이 눈에 잘 띔, 사이트의 의도 "너가 게시글을 작성했으면 좋겠어.")
### 좋은 인터렉션을 넣고 싶다면,
- 같은 도메인의 사이트를 전부 써보고, 원하는 인터렉션이 명확하다면 다른 도메인의 사이트도 참고해보면 좋다.
