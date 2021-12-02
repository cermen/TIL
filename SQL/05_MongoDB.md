# MongoDB

### 개요

- Not only SQL(NoSQL)
- 정해진 규칙이 없다(Schema X)
- join 없음
- key / value 이루어진 데이터를 담는다
- Database - Collection(table) - Document(row)

### 명령어

- `show dbs` : 전체 DB 표시
- `use db_name` : 해당 DB 사용
- `show collections` : 전체 테이블 표시

#### 입력

- `db.collection_name.insertOne({key: value, key: value})` : 1개의 document를 삽입
- `db.collection_name.insertMany({key: value, key: value}, {key: value, key: value})` : 여러 개의 document를 삽입

#### 검색

`db.user.find({condition}, {column list})`

- `db.user.find()`

  => select * from user;

- `db.user.find({}, {user_id: 1, _id: 0})` 

  => select user_id from user;

- `db.user.find({gender: 'f'}, {}) `

  => select * from user where gender='f';

- `db.user.find({gender: 'f', user_id: 'jyu'}, {}) `

  => select * from user_id='jyu' and gender='f';

- `db.user.find({gender: 'f'}, {user_id: 'jyu'}) `

  => select from user where;

- `db.user.find({$or: [{gender: 'f'}, {user_id: 'jslim'}]}, {})`

  => select * from user where user_id=xxxx or gender=xxxx

**논리 연산자** - `$not`, `$or`, `$and`, `$nor`

**비교 연산자**

- `$eq` : = (equals)
- `$ne` : != (not equals)
- `$gt` : > (greater than)
- `$gte`: >=  (greater than or equals)
- `$lt` : < (least than)
- `$lte`: <= (least than or equals)
- `$in` : 주어진 배열 안에 속하는 값
- `$nin` : 주어진 배열 안에 속하지 않는 값 (not in)

#### 수정

- `db.collection_name.updateOne({condition}. {$set}` : 1개의 document를 수정
- `db.collection_name.updateMany({condition}. {$set})` : 여러 개의 document를 수정

- ex) `db.user.updateOne({user_id: 'jslim'}, {$set: {gender: f}})`
  => update  user set	gender='f'  where   user_id='jslim';

#### 삭제
- `db.collection_name.removeOne({where}}` : 1개의 document를 삭제
- `db.collection_name.removeMany()` : 전체 document를 삭제