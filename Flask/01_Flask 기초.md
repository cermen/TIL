# Flask 기초

```python
from flask import Flask
app = Flask(__name__)


@app.route('/')
def hello():
    return '<h1>Hello Flask!</h1>'


@app.route('/subpage')
def sub_page():
    return 'This is sub page'


if __name__ == '__main__':
    app.run(host='127.0.0.1', port=8081)
```



## Flask로 REST API 구현하기

- 클라이언트에서 요청(Request)를 보내면
  서버에서 응답(Respose)를 준다.

### REST

- 자원의 표현에 의한 상태 전달
- HTTP URI를 통해 자원을 명시하고, HTTP 메소드를 통해 자원에 대한 CRUD 연산 적용

#### CRUD 연산과 HTTP 매소드

- Create : 생성(POST)
- Read : 조회(GET)
- Update : 수정(PUT)
- Delete : 삭제(DELETE)

#### flask.jsonify 함수

리턴 데이터를 JSON 포맷으로 제공

**예시**

```python
from flask import Flask, jsonify

app = Flask(__name__)

@app.route('/json_test')
def hello_json():
    data = {'name': 'jyu', 'age': 29}
    return jsonify(data)


@app.route('/server_info')
def server_json():
    data = {'server_name': '127.0.0.1', 'server_port': 8081}
    return jsonify(data)
```

