# ES6

#### ECMAScript(ES)

ECMA International에서 지정한 자바스크립트 언어 표준. 1997년에 첫 버전이 발표되었으며, 2015년에 발표된 ES6 이후로 매년 발표하고 있다.

#### ES6에서 추가된 것

- 화살표 함수가 추가되었다.

  ```js
  const hello = (name) => {
      return "Hello " + name;
  }
  ```

- 블록 레벨 스코프를 가진 `let`과 `const`가 추가되어 호이스팅을 방지하게 되었다.

- `for-of`문과 `for-in`문이 추가되었다.

- `` `(백틱)을 사용하여 문자열을 편리하게 관리할 수 있게 되었다.

  - Template literal 추가
    `parseInt(year) + '년 ' + parseInt(month) + '월 ' + parseInt(day) + '일'`
    → `${year}년 ${month}월 ${day}일` (앞뒤에 `` `(백틱)을 붙인다.)

  - multi-line string 지원

    ```js
    // ec5
    var hello = "Hello everyone!\n" + 
        		"This is JavaScript.";
    // ec6
    const hello = `Hello everyone!
        		This is JavaScript.`;
    ```

- 클래스가 추가되어 객체지향 프로그래밍을 지원할 수 있게 되었다.

- 모듈이 추가되어 파일 분리가 가능해졌다.

- promise가 도입되어 비동기 처리를 효과적으로 할 수 있게 되었다.