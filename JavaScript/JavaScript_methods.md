## JavaScript 주요 메소드

#### 문자열 관련 메소드

- `String.length` : 문자열의 길이를 반환
- `String.prototype.split(tok)` : 문자열을 구분자에 따라 분리
- `String.prototype.includes(substr)` : `substr`이 문자열에 포함되어 있는지를 True/False로 반환
- `String.prototype.indexOf(val)` : 문자열에서 지정된 값을 찾을 수 있는 맨 앞의 인덱스를 반환하며, 존재하지 않을 경우 -1을 반환한다. 
- `String.prototype.charAt(index)` : 문자열의 특정 인덱스의 값을 반환
- `String.prototype.slice(start, end)` : 문자열의 `start` 인덱스부터 `end` 직전 인덱스까지의 부분 문자열을 반환  ex) 
- `String.prototype.repeat(times)` : 문자열을 `times`번 반복하여 반환
- `String.toLowerCase(str)` : 해당 문자열을 모두 소문자로 바꾸는 메소드
- `String.toUpperCase(str)` : 해당 문자열을 모두 대문자로 바꾸는 메소드
- `String.replace(sub1, sub2)` : 문자열의 특정 부분을 다른 문자로 바꾸는 메소드
- `String.charCodeAt(index)` : 문자열의 해당 인덱스의 유니코드를 반환
- `String.fromCharCode(code)` : 유니코드에 해당하는 문자를 반환

#### 배열 관련 메소드

- `Array.length` : 문자열의 길이를 반환
- `Array.prototype.includes(val)` : 특정 값이 배열에 있는지를 True/False로 반환
- `Array.prototype.push(val)` : 특정 값을 배열에 첨가하는 메소드
- `Array.prototype.pop()` : 배열의 맨 마지막 값을 삭제하여 반환
- `Array.prototype.indexOf(val)` : 배열에서 지정된 값을 찾을 수 있는 맨 앞의 인덱스를 반환하며, 존재하지 않을 경우 -1을 반환한다. 
- `Array.prototype.reverse()` : 배열의 순서를 역순으로 반환한다.

- `Array.prototype.join(tok)` : 배열의 요소를 묶어 한 문자열로 만드는 메소드

  - `tok`이 정의되지 않을 경우 `,`로 묶인다.

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

- `Array.prototype.splice()` : 배열의 요소를 삭제 또는 교체하기나 새 요소를 추가하는 메소드


#### 형변환 메소드

- `parseInt(num)` : 문자열을 정수로 변환
- `parseFloat(num)` : 문자열을 실수로 변환
- `Number.prototype.toString()` : 숫자를 문자열로 변환

#### 수학 관련 메소드

- `Math.min([numbers])` : 주어진 숫자 중 가장 작은 값을 반환한다.
- `Math.max([numbers])` : 주어진 숫자 중 가장 큰 값을 반환한다.
- `Math.sqrt(num)` : 주어진 숫자의 제곱근을 반환한다.
