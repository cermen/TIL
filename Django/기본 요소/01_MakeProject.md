## django 프로젝트 생성

1. 프로젝트를 만든다.
2. django 패키지를 설치한다.

3. `django-admin startproject web이름` 명령어를 입력한다.

4. settings.py 파일에서 `ALLOWED_HOSTS`를 설정한다.
    `ALLOWED_HOSTS = ['localhost', '127.0.0.1']`

5. TIME_ZONE을 설정한다.
    `TIME_ZONE = 'Asia/Seoul'`

6. 터미널로 web 폴더로 들어가서 서버를 실행한다.
   - `python manage.py runserver` 명령어 입력
   - 서버 종료 : ctrl+c

7. 새로운 app 설치
   `python manage.py startapp app이름` 명령어 입력

8. web/settings.py의 `INSTALLED_APPS` 변수에 새 app 이름을 입력한다.

9. web/urls.py에 `django.urls.include`를 import하고
   `urlpatterns`에 `path('front/', include('app이름.urls'))`를 추가한다

10. app 폴더에 urls.py 파일을 생성하여 web/urls.py의 내용을 복사한 후 다음과 같이 수정한다.

    ```python
    from django.contrib import admin
    from django.urls import path, include
    from app이름 import views

    urlpatterns = [
        path('main/', views.index)
    ]
    ```

11. app/views.py 파일에 다음 내용을 추가한다.

    ```python
    def index(request):
    	print('request index - ')
        return render(request, )
    ```

12. app 패키지에 templates 디텍토리를 추가하여 그곳에 html 파일을 생성한다.

13. app/views.py 파일을 다음과 같이 수정한다.

    ```python
    def index(request):
        print('request index - ')
        return render(request, 'frontDemo.html')
    ```

#### 장고 개발 흐름

<img src='img/장고 개발 흐름.png'>

1. 웹 브라우저 주소창에 localhost:8000/app이름 입력(장고 개발 서버에 /app이름 페이지 요청).
2. config/urls.py 파일에서 URL을 해석해 app이름/views.py 파일의 index 함수 호출.
3. app이름/views.py 파일의 index 함수를 실행하고 그 결과를 웹 브라우저에 전달.

(출처 : https://wikidocs.net/70649)