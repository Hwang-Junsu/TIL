# Browser ?
- 엄청 많은 기능을 가진 고도화된 어플리케이션, 자바스크립트는 이 브라우저에서 사용하기 위해 만들어졌다.

![browser](https://teamsparta.notion.site/image/https%3A%2F%2Fs3-us-west-2.amazonaws.com%2Fsecure.notion-static.com%2F282fddb4-ba1f-4c3b-9b50-6430aff65724%2Fimage002.png?table=block&id=b168ee0b-77cb-484f-93cd-b4f526e9c0f7&spaceId=83c75a39-3aba-4ba4-a792-7aefe4b07895&width=770&userId=&cache=v2)   

- 사용자 인터페이스 : 주소 표시줄, 이전/다음 페이지 버튼, 북마크, 새로고침 버튼 등
- 브라우저 엔진 : 사용자 인터페이스와 렌더링 엔진 사이의 동작을 제어
- 렌더링 엔진 : 화면을 창에 보여줌
- 통신 : HTTP같은 프로토콜을 이용해서 서버에 요청을 보내는 등에 사용
- UI 백엔드 : 얼럿 창, 셀렉트 박스, 콤보 박스 등을 OS 별로 그림
- 자바스크립트 해석기 : 자바스크립트를 해석하고 실행
- 자료 저장소 : Cookie, Local Storage, Session Storage 등 데이터 저장

# Rendering Engine
- 파싱 단계 : DOM 트리와 CSSOM 트리를 만듭니다.
- 렌더 트리 단계 : DOM과 CSSOM을 묶어서 렌더 트리를 만듭니다.
- 레이아웃 단계 : 렌더 트리에서 각 노드가 어디에 어떻게 그려져야 하는 지 모양을 계산합니다.
- 페인트 단계 : 계산한대로 화면에 엘리먼트들을 배치합니다. (페인팅 한다고 함.)

# DOM
DOM(Document Object Model)
MDN 문서에서는 아래와 같이 설명합니다. 

[문서 객체 모델(The Document Object Model, 이하 DOM) 은 HTML, XML 문서의 프로그래밍 interface 이다. DOM은 문서의 구조화된 표현(structured representation)을 제공하며 프로그래밍 언어가 DOM 구조에 접근할 수 있는 방법을 제공하여 그들이 문서 구조, 스타일, 내용 등을 변경할 수 있게 돕는다. DOM 은 nodes와 objects로 문서를 표현한다. 이들은 웹 페이지를 스크립트 또는 프로그래밍 언어들에서 사용될 수 있게 연결시켜주는 역할을 담당한다.]

웹페이지는 document고, document는 객체. DOM은 웹페이지의 모든 콘텐츠를 객체로 나타냅니다.  그리고 이 객체는 수정이 가능하다. 
document 객체를 사용해 웹 페이지 내의 무엇이든 변경할 수 있다는 이야기.

# BOM
BOM(Browser Object Model) 
navigator, location 같은 객체, 이런 객체들은 브라우저가 제공하는 추가 객체입니다. 호스트 환경을 자바스크립트가 돌아가는 플랫폼인데,
BOM은 호스트인 브라우저가 제공하는 추가 객체를 말합니다. 
navigator, location외에도 confirm, alert 등이 BOM의 일부.
confirm, alert 등은 사용자와 브라우저 사이의 원활한 소통을 도와주는 순수한 브라우저 메서드임.

# CSSOM
CSS는 HTML하고는 다른 구조를 가지고 있음.
CSS만의 문법, 규칙을 스타일 시트를 객체로 나타냅니다. DOM이 웹 페이지를 객체로 나타내는 것과 같다.
