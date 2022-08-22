# 동기? 비동기?
- 동기는 동시에 일어나는 일, 비동기는 동시에 일어나지 않는 일이라고 생각하면 편함.
- 자바스크립트는 싱글 쓰레드(프로세스 내에서 실제로 작업을 수행하는 주체)로 동작하는 언어.
- 자바스크립트는 기본적으로는 동기방식으로 처리하지만, 비동기도 가능.
- run to completion 방식(메시지 처리가 시작되면 이 메시지의 처리가 끝날 때까지는 다른 어떤 작업도 중간에 끼어들지 못한다는 의미)  
 
 
 # 동시성
 - V8 엔진에서의 비동기 작업 처리
 ![IMG](https://teamsparta.notion.site/image/https%3A%2F%2Fs3-us-west-2.amazonaws.com%2Fsecure.notion-static.com%2F0d4b45d4-c3d5-4cb0-9571-241cebe6f5fb%2Fevent-loop.png?table=block&id=4c608423-9785-453c-9ee3-7ea5743b0e65&spaceId=83c75a39-3aba-4ba4-a792-7aefe4b07895&width=770&userId=&cache=v2)
 - 자바스크립트는 기본적으로 한번에 하나의 일만 처리하지만, 여러작업이 한 번에 처리되는 것 처럼 보이는 것을 `동시성` 이라고 함.
 - 용어 정리
    - heap : 동적으로 생성된 객체 인스턴스가 할당되는 영역
    - call stack : 일거리가 쌓이는 스택
    - event queue : 테스크 큐(Task queue)나 콜백 큐(callback queue)라고도 함. 비동기 처리 함수의 콜백 함수, 비동기식 이벤트 핸들러, 타이머의 콜백 함수를 넣어두는 큐
    - event loop : 테스크(일거리)가 들어오길 기다렸다가 테스크가 들어오면 일을 하고, 일이 없으면 잠깐 쉬기를 반복하는 자바스크립트 내의 루프
    **→ call stack 내에서 현재 실행중인 일거리가 있는 지, 이벤트 큐에 일거리가 있는 지 반복해서 확인하고, 콜 스택이 비어 있으면 이벤트 큐의 일거리를 콜스택으로 옮겨가게끔 돕는다.**
    - Web API : Ajax, DOM event, setTimeout 등 브라우저에 내장된 API
