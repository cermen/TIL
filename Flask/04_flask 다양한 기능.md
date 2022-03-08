# flask 다양한 기능

### 에러 다루기

- `errorhandler` 데코레이터를 사용하여 HTTP 오류 코드가 나오는 페이지를 정의

```python
from flask import Flask

@app.errorhandler(404)
def page_not_founded(error):
    return '<h1>404 Error</h1>'
```

### 로깅 다루기

- 서버에 문제가 있을 때 어떤 문제가 있었는지 파악하기 위해 로깅 기능을 사용함
- 파이썬에는 로그를 다루는 `logging` 라이브러리가 있음

#### 주요 logging 핸들러

- `FileHandler` : 파일로 로그를 저장
- `RotatingFileHandler` : 파일로 로그를 저장하되, 파일이 정해진 사이즈를 넘어가면 새로운 파일로 생성
  - `RotatingFileHandler(maxBytes=하나의파일사이즈, backupCount=파일개수)`
  - 전체 파일을 다 쓰면, 다시 처음부터 씀
- `NTEventLogHandler` : 윈도우 시스템 로그로 남김
- `SysLogHandler` : 유닉스 계열 시스템의 syslog로 남김



### 다양한 데코레이터

- `before_first_request` : 웹 애플리케이션 기동 이후 가장 처음에 들어오는 HTTP 요청에서만 실행
- `before_request` : HTTP 요청이 들어올 때마다 실행
  - 위 2게는 인자를 전달할 수는 없음
- `after_request` : HTTP 요청 처리가 끝나고 브라우저에 응답하기 전에 실행
  - response를 리턴해야 함