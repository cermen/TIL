# JSX

JavaScript의 확장 문법으로, JS에서 XML 형식의 값을 반환할 수 있도록 한다.

#### 주요 JSX 문법

- HTML의 `class` 대신 `className`을 사용한다.
  (이는 JS의 `class` 문과 혼동을 막기 위해서이다.)
- 변수를 HTML에 삽입할 때 중괄호`{}`를 사용한다.
- HTML에 속성을 삽입할 때 `속성={ {속성명: 속성값} }`을 사용한다.
  - CSS 속성 중 `-`로 구분된 것(`font-size` 등)은 camelCase 형태로 써야 한다.
- 반환값은 한 개의 div 태그로 감싸져 있어야 한다.

#### 예제

```react
function App() {
  let post = '리액트 수강 시작!';
  return (
    <div className="App">
      <div className='black-nav'>
        <h4 style={ {color: 'red', fontSize: '16px'} }>My blog</h4>
      </div>
      <h4>{ post }</h4>
    </div>
  );
}
```
