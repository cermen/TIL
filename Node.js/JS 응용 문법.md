# JS 응용 문법

### Node.js 개요

- 자바스크립트가 브라우저가 아닌 곳에서도 실행될 수 있게 도와주는 런타임 플랫폼
- 구글 V8 엔진을 기반으로 개발되었다.

#### npm

- 자바스크립트에서 사용할 수 있는 패키지 관리자
  (파이썬의 pip와 같은 기능을 한다.)

#### REPL

- 자바스크립트 문장을 즉석에서 실행할 수 있게 해주는 프로그램
- 크롬 등의 브라우저에 콘솔로 내장되어 있다.

### 함수 응용

#### 익명 함수

- 일반 함수와는 다르게 함수의 이름이 존재하지 않고 변수에 함수를 담아 사용하는 함수이다.

```js
let hello = function () {
  console.log("Hello world!");
};
```

#### 화살표 함수

- 화살표 모양을 한 함수로, 기존 함수보다 더 간결한 문법을 만들 수 있다.
  (Python의 lambda 함수, C++의 인라인 함수와 같은 기능을 한다.)
- ES6부터 추가되었다.

```js
const sum = (a, b) => {
	return a + b;
};
```

- `return`을 생략해서 사용할 수 있다.

```js
const sum = (a, b) => a + b;
```

- 하나의 인자를 입력받는 경우에는 괄호를 생략할 수 있다.

```js
const hello = a => {
	return a;
};
```



#### 동기와 비동기

- **동기 실행**: 먼저 실행된 코드의 결과가 나올 때까지 대기하는 것
- **비동기 실행**: 실행된 순서와 관계 없이 결과가 나오는 것

#### Blocking model과 Non-Blocking model

- **Blocking model**: 코드의 실행이 끝나기 전까지 실행 제어권을 다른 곳에 넘기지 않아 다른 작업을 하지 못하고 대기하는 모델 - 비동기 처리가 불가능함
- **Non-Blocking model**: 코드의 실행이 끝나지 않아도 실행 제어권을 다른 곳에 넘겨 다른 코드가 실행되도록 하는 모델 - 비동기 처리가 가능함
- 자바스크립트는 비동기와 Non-Blocking model을 사용하여 현재 코드의 실행이 끝나지 않아도 다음 코드를 호출할 수 있다.

**예사**

```js
function first() {
  console.log('First');
}

setTimeout(first, 1000); // 1000ms(1초) 뒤에 first 함수를 실행해준다.

console.log('Middle');
console.log('Last');

/* print */
// Middle
// Last
// First
```

#### Promise

- 자바스크립트에서 비동기 처리를 동기로 처리할 수 있게 돕는 객체 유형

```js
new Promise(executor);	// executor에는 함수만 올 수 있다.

// 예제
new Promise((resolve, reject) => {
	// 명령문
});
```

- 프로미스가 만들어 질 때 `executor`가 실행되며, `executor`에서 `resolve` 함수가 호출되기 전까지 `firstPromise.then(...)` 안에 있는 코드를 실행하지 않는다.

##### 프로미스의 상태

- 대기(*Pending)*: 이행하거나 거부되지 않은 초기 상태.
- 이행(*Fulfilled)*: 연산이 성공적으로 완료됨.
- 거부(*Rejected)*: 연산이 실패함.

#### 비동기 함수

- 비동기 함수는 일반 함수나 화살표 함수와 비슷하지만 두 가지가 다르다.

  - 비동기 함수의 결과 값은 항상 Promise 객체로 resolve된다.

  - 비동기 함수 안에서만 await 연산자를 사용할 수 있다.

- 결과 값은 Promise로 받는다.

```js
// 비동기 + 일반 함수
async function 함수이름() {
	// 명령문
}

// 비동기 + 익명 함수
async function() {
  // 명령문
}

// 비동기 + 화살표 함수
async () => {
	// 명령문
}
```

#### await 연산자

- await 연산자를 사용하면 Promise가 fulfill되거나 rejected될 때 까지 함수의 실행을 중단하고 기다릴 수 있다.
- 비동기 함수 안에서만 사용할 수 있다.
- 값에는 Promise가 아닌 다른 값도 들어갈 수 있다.

```js
const result = await 값;
```

### 