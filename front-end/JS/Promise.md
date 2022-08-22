# Callback
- callback은 특정 함수에 매개변수로 전달된 함수.
- 자바스크립트가 비동기 처리를 하기 위한 패턴 중 하나.
- 전통적인 콜백 패턴은 일명 콜백 지옥(callback hell) 문제가 생기기 쉽다.
- 꼬리에 꼬리를 무는 비동기 처리가 늘어나면 호출이 계속 중첩되고, 관리가 어려워짐.

# Promise
- 전통적인 콜백 패턴으로 인한 콜백 지옥 때문에 ES6에서 도입한 비동기 처리 패턴.
- 비동기 연산이 종료된 이후에 결과를 알기 위해 사용하는 객체.
- 프라미스를 쓰면 비동기 메서드를 마치 동기 메서드처럼 값을 반환할 수 있다.
- 외부 api를 받게 되는 상황일 때 등등, 많이 사용할 것임.

```javascript
const promise = new Promise((resolve, reject) => {
  if(...> {
    ...
    resolve("성공!);
  } else {
    ...
    reject("실패!");
  }
});
```
- 생성자 함수를 통해 생성, 비동기 작업을 수행할 콜백 함수를 인자로 받아서 사용한다.
- Promise state
  - pending: 비동기 처리 수행 전(resolve, reject가 아직 호출되지 않음)
  - fulfilled: 수행 성공(resolve가 호출된 상태)
  - rejected: 수행 실패(reject가 호출된 상태)
  - settled: 성공 or 실패(resolve나 reject가 호출된 상태)

## Promise 후속 처리 메서드
- promise로 구현된 비동기 함수를 호출하는 측에서는 이 프로미스 객체의 후속 처리를 메서드를 통해 비동기 처리 결과(성공 결과나, 에러 메시지)를 받아서 처리해야 함.
- .then(성공 시, 실패 시)
```javascript
// 프라미스를 하나 만들어 봅시다!
let promise = new Promise((resolve, reject) => {
	setTimeout(() => reject(new Error("오류!")), 1000);
});
// reject
promise.then(result => {
	console.log(result); // 실행되지 않습니다.
}, error => {
	console.log(error); // Error: 오류!가 찍힐거예요.
});
```
- .catch(실패 시)
```javascript
// 프라미스를 하나 만들어 봅시다!
let promise = new Promise((resolve, reject) => {
	setTimeout(() => reject(new Error("오류!"), 1000);
});

promise.catch((error) => {console.log(error};);
```
## Promise Chaning
- 프로미스는 후속 처리 메서드를 체이닝 해서 여러개의 프라미스를 연결할 수 있다.

```jsx
new Promise((resolve, reject) => {
	setTimeout(() => resolve("promise 1"), 1000);
}).then((result) => { // 후속 처리 메서드 하나를 쓰고,
	console.log(result); // promise 1
	return new Promise(...);
}).then((result) => { // 이렇게 연달아 then을 써서 이어주는 거예요.
	console.log(result);
	return new Promise(...);
}).then(...);
```

