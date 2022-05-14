## JavaScript 주요 메소드

#### 문자열 관련 메소드

- `String.length` : 문자열의 길이를 반환
- `String.prototype.includes(substr)` : `substr`이 문자열에 포함되어 있는지를 True/False로 반환
- `String.prototype.charAt(index)` : 문자열의 특정 인덱스의 값을 반환
- `String.prototype.slice(start, end)` : 문자열의 `start` 인덱스부터 `end` 직전 인덱스까지의 부분 문자열을 반환  ex) 
- `String.prototype.repeat(times)` : 문자열을 `times`번 반복하여 반환

#### 배열 관련 메소드

- `Array.length` : 문자열의 길이를 반환
- `Array.prototype.includes(val)` : 특정 값이 배열에 있는지를 True/False로 반환
- `Array.prototype.push(val)` : 특정 값을 배열에 첨가하는 메소드
- `Array.prototype.pop()` : 배열의 맨 마지막 값을 삭제하여 반환
- `Array.prototype.indexOf(val)` : 배열에서 지정된 값을 찾을 수 있는 맨 앞의 인덱스를 반환하며, 존재하지 않을 경우 1을 반환한다. 
- `Array.prototype.reverse()` : 배열의 순서를 역순으로 반환한다.

- `Array.prototype.sort(func)` : 배열을 정렬하는 메소드이다.

  - `func` : 비교 기준을 정하는 함수
    주어지지 않을 경우 유니코드 문자열 순서에 따라 배열한다.

  - 숫자를 배열할 경우에는 아래와 같이 사용한다.

    ```js
    answer.sort(function(a, b) {
        return a - b;
    });
    ```

- `Array.prototype.map(func)` : 배열의 모든 요소에 해당 함수를 적용하는 메소드

#### 형변환 메소드

- `parseInt(num)` : 문자열을 정수로 변환
- `parseFloat(num)` : 문자열을 실수로 변환
- `Number.prototype.toString()` : 숫자를 문자열로 변환

