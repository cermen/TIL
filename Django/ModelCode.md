# MongoDB 쿼리 정리

### 삽입 (Create)

- 한 개 삽입: `db.collection.insertOne(<doc>)`
- 여러 개 삽입: `db.collection.insertMany({<doc1>, <doc2>, ...})`

### 검색 (Read)

`db.collection.find({조건})`를 사용한다.

### 수정 (Update)

- 한 개 수정: `db.collection.updateOne({조건}, {$set: {}})`
- 여러 개 수정: `db.collection.updateMany({조건}, {$set: {}})`

### 삭제 (Delete)

- 한 개 삭제: `db.collection.deleteOne({조건})`
- 여러 개 삭제: `db.collection.deleteMany({조건})`



| SQL 쿼리                                              | MongoDB 쿼리                                                 |
| ----------------------------------------------------- | ------------------------------------------------------------ |
| `select * from table;`                                | `db.collection.find({})`;                                    |
| `select * from table where id = xxxx;`                | `db.collection.find({id: xxxx})`                             |
| `select * from table where id = xxxx and pwd = xxxx;` | `db.collection.find({id: xxxx, pwd: xxxx})`                  |
| `select * from table where id = xxxx or pwd = xxxx;`  | `db.collection.find($or: [{id: xxxx}, {pwd: xxxx}])`         |
|                                                       |                                                              |
|                                                       |                                                              |
|                                                       |                                                              |
| `insert into table values()`                          | `db.collection.insertOne()`<br />`db.collection.insertMany()` |
| `update tableName set attr = value where id = xxxxx`  | `db.collection.updateOne()`<br />`db.collection.updateMany()` |
| `delete * from tableName where id = xxxx`             | `db.collection.updateOne()`<br />`db.collection.updateMany()` |
