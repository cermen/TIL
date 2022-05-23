# Express.js 기초

### HTTP

- 데이터를 주고 받는 양식을 정의한 통신 규약 중 하나로, 세계에서 가장 널리 쓰이는 규약이다.
- HTTP에서는 Request와 Response를 통해 데이터를 주고받는다.
  - 브라우저는 서버에게 자신이 원하는 페이지의 정보를 요구한다 - **Request**
  - 서버는 브라우저가 원하는 페이지가 있는지 확인하고, 있으면 해당 페이지에 대한 데이터를 보낸다. - **Response**
    없으면 빈 데이터를 반환한다.

#### HTTP의 메소드

- `GET` : 데이터를 받을 때 사용한다.
- `POST` : 데이터를 게시할 때 사용한다.

### Express.js

Node.js로 서버를 빠르고 간편하게 만들 수 있게 도와주는 웹 프레임워크

**코드 예시**

```js
const express = require('express');
const app = express();
const port = 3000;

// root 주소의 페이지에서 'Hello World!' 출력
app.get('/', (req, res) => {
	res.send('Hello World!');
});

app.listen(port, () => {
	console.log(port, '포트로 서버가 열렸어요!');
});
```

### 미들웨어

>  운영 체제와 응용 소프트웨어의 중간에서 조정과 중개의 역할을 수행하는 소프트웨어

- Express.js에는 urlencoded, json 등이 있다.

#### 미들웨어 템플릿

```js
app.use((req, res, next) => {
    // 필요한 코드
});
```

- `req` : 요청에 대한 정보가 담겨 있는 객체
- `res` : response 객체 - 응답을 위한 기능이 제공된다.
- `next` : 다음에 작동할 미들웨어

### Routing과 Router

>  **라우팅**(Routing): 클라이언트의 요청 조건에 대응에 응답하는 방식

#### Express.js의 라우터

- routes 폴더 안의 파일에 정의한다.

```js
// routes/goods.js
const express = require('express');
const router = express.Router();

router.get('/', (req, res) => {
	res.send('this is home page');
});

router.get('/about', (req, res) => {
	res.send('this is about page');
});
```

### REST API

> **API**(Application Programming Interface): 애플리케이션끼리 연결해주는 매개체

**REST**(Representational State Transfer): 소프트웨어 아키텍처의 한 형식으로, URL, Headers, Method 등 네트워크 표현 수단을 사람이 봐도 이해하기 쉬운 표현으로 정의한다.

#### REST API의 3가지 구성 요소

1. 자원(Resource): URL
2. 행위: HTTP Method - POST, GET, PUT, DELETE (각각 CRUD에 해당됨)
3. 표현: 해당 표현을 어떻게 할 것인지에 대한 설명

**예시**

```js
router.get('/books', (req, res) => {
	res.json({ success: true, data: getAllBooks() });
});
```
