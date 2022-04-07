# Flask 기본

### 프레임워크

- 자주 사용되는 코드를 체계화하여 쉽게 사용할 수 있도록 도와주는 코드 집합
- 라이브러리와 혼동될 수 있지만 좀 더 규모가 크고 프로젝트의 기반이 됨
- 건축에 비유하면 구조를 만드는 골조가 프레임워크라면 그 외 자재들이 라이브러리가 됨

### Flask의 특징

- 마이크로 웹 프레임워크로, 특별한 도구나 라이브러리가 필요 없다. => 가벼운 프레임워크
- 자유도가 높다.

#### 예제 코드

```python
# app.py
from flask import Flask
app = Flask(__name__)

@app.route('/')
def hello():
    return 'Hello world!'
```

cmd에서 `flask run`을 입력하면 코드가 실행되며, 이 상태에서 웹 브라우저로 접속하면 화면에 \'Hello world!\'가 출력된다.

### MVC

> Model-View-Controller - 디자인 패턴 중 하나

- Model: 데이터베이스와 연결되는 부분
- View: 클라이언트가 보는 부분
- Controller: 접근 URL에 따라 비즈니스 로직이 수행되는 부분

### SQLAlchemy

- 파이썬에서 사용하는 ORM이다.
  - ORM(Object-relational maping): 데이터베이스의 객체와 관계를 연결해 주는 것

#### 사용 예제

```python
import os
from flask import Flask
from flask_sqlalchemy import SQLAlchemy

basedir = os.path.abspath(os.path.dirname(__file__))
dbfile = os.path.join(basedir, 'db.sqlite')

app = Flask(__name__)
app.config['SQLALCHEMY_DATABASE_URI'] = 'sqlite:///' + dbfile
app.config['SQLALCHEMY_COMMIT_ON_TEARDOWN'] = True
app.config['SQLALCHEMY_TRACK_MODIFICATIONS'] = False

db = SQLAlchemy(app)

class Test(db.Model):
    __tablename__ = 'test_table'
    id = db.Column(db.Integer, primary_key=True)
    name = db.Column(db.String(32), unique=True)
```

