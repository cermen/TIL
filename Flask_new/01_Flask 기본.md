# Flask 기본

## 프레임워크

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
