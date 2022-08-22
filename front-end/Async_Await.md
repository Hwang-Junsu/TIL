# async, await
- ES8에 나온 키워드.
- 프로미스를 편하게 쓸 수 있게 만들어주는 문법.

## 1. async
- 함수 앞에 async를 붙여서 사용하고, 항상 프로미스를 반환한다.(프로미스가 아니어도 프로미스로 감싸서 반환함.)
```javascript
// async는 function 앞에 써줍니다.
async function myFunc() {
	return "프라미스를 반환해요!"; // 프라미스가 아닌 걸 반환해볼게요!
}

myFunc().then(result => {console.log(result)}); // 콘솔로 확인해봅시다!
```

## 2. await
- async의 짝꿍. async 함수 안에서만 동작한다.
- await는 프로미스가 처리될 때 까지 기다렸다가 그 이후에 결과를 반환한다.

```javascript
async function myFunc(){
	let promise = new Promise((resolve, reject) => {
		setTimeout(() => resolve("완료!"), 1000);
	});

    console.log(promise);

	let result = await promise; // 여기서 기다리자!하고 신호를 줍니다.

    console.log(promise);

	console.log(result); // then(후처리 함수)를 쓰지 않았는데도, 1초 후에 완료!가 콘솔에 찍힐거예요.
}

```
