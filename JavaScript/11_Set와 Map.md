# Set와 Map

### 세트

중복을 허용하지 않는 이터레이터

```js
const set = new Set([1, 2, 2, 3, 3, 4]);
console.log(set);	// Set(4) { 1, 2, 3, 4 }
```

#### Set 메소드

- `Set.prototype.size` : set의 크기
- `Set.prototype.add(val)` : set에 값 추가
- `Set.prototype.delete(val)` : set의 값 삭제
- `Set.prototype.clear()` : set의 값 전부 삭제

### 맵

키-값(Key-Value) 쌍을 나타내는 집합

```js
const map = new Map([
    ['key1', '사과'],
    ['key2', '바나나'],
])
console.log(map);	// Map(2) { 'key1' => '사과', 'key2' => '바나나' }
```

#### 객체와의 차이

- 키를 문자형으로 변환하지 않는다.

#### Map 메소드

- `Map.prototype.size` : map의 크기
- `Map.prototype.keys()` : key 반환
- `Map.prototype.values()` : value 반환
- `Map.prototype.entries()` : key, value 모두 반환
- `Map.prototype.has(key)` : map에 해당 key가 존재하는지 확인
- `Map.prototype.get(val)` : map의 해당 key의 값 반환
- `Map.prototype.add(val)` : map에 값 추가
- `Map.prototype.delete(val)` : set의 값 삭제
- `Map.prototype.clear()` : set의 값 전부 삭제

### 심볼형

유일한 키를 생성할 때 사용한다.

```js
const map = new Map();
// const key1 = 'key';
// const key2 = 'key';
const key1 = Symbol('key');
const key2 = Symbol('key');
map.set(key1, 'hello');
console.log(map.get(key2));
console.log(key1 === key2);     // false
```

#### Symbol.for

동일한 이름으로 하나의 키를 사용하고 싶을 때 사용한다.

```js
const k1 = Symbol.for('key');
const k2 = Symbol.for('key');
console.log(k1 === k2);         // true
```

