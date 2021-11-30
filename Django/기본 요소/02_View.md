# URL과 뷰

#### urls 파일 

>  URL을 매핑하는 파일

- `django.urls.path()` : URL 매핑 추가 함수
  `path(url주소, view함수)`

```python
# configs\urls.py
from django.contrib import admin
from django.urls import path
from pybo import views

urlpatterns = [
    path('admin/', admin.site.urls),
    path('pybo/', views.index),
]
```

#### views 파일

> 홈페이지의 로직을 구성하는 파일

- `django.http.HttpResponse()` : 페이지 요청에 대한 응답을 할 때 사용하는 장고 클래스
  `HttpResponse(문자열)`

```python
# pybo\views.py
from django.http import HttpResponse

def index(request):
    return HttpResponse("안녕하세요 pybo에 오신것을 환영합니다.")
```

#### URL 파일 분리

```python
# configs\urls.py
from django.contrib import admin
from django.urls import path, include

urlpatterns = [
    path('admin/', admin.site.urls),
    path('pybo/', include('pybo.urls')),
]
```

```python
# pybo\urls.py
from django.urls import path

from . import views

urlpatterns = [
    path('', views.index),
]
```

