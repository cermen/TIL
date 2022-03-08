# flask_login 라이브러리

> 사용자를 체크하는 기능을 담당하는 라이브러리

### 주요 동작 방식

1. 사용자가 로그인하면, 로그인 정보를 User class에서 객체로 가져오고, LoginManager()에 추가하여 세션 생성
   - flask 서버가 return 시에 해당 세션 정보를 웹페이지에 송부
2. current_user 객체에 해당 객체가 저장됨
3. 로그인 후 웹페이지로 flask 서버 접근 시, 전달받은 세션 정보를 기반으로 접근
4. 사용자가 로그아웃시 LoginManager()에서 해당 id 제거