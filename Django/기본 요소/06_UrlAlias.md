## URL 별칭

urls.py 안의 URL 규칙이 바뀌면 템플릿 안에 있는 링크값을 모두 바꿔줘야 함 
→ 이를 해결하기 위해 URL 별칭을 사용한다.

```python
# pybo/urls.py
from django.urls import path

from . import views

app_name = 'pybo'

urlpatterns = [
    path('', views.index, name='index'),
    path('<int:question_id>/', views.detail, name='detail')
]
```

```html
<!-- templates/pybo/question_list.html -->
<body>
    <!-- 생략 -->
        {% for question in question_list %}
        <li><a href="/pybo/{{% url 'detail' question.id %}}/">{{ question.subject }}</a></li>
        {% endfor %}
    <!-- 생략 -->
</body>
```



pybo 이외의 다른 앱이 추가될 때 서로 다른 앱에서 같은 URL 별칭을 사용하면 중복 문제가 생긴다.
→ 네임스페이스(namespace)를 추가한다.

```html
<!-- templates/pybo/question_list.html -->
<body>
    <!-- 생략 -->
        {% for question in question_list %}
        <li><a href="/pybo/{{% url 'pybo:detail' question.id %}}/">{{ question.subject }}</a></li>
        {% endfor %}
    <!-- 생략 -->
</body>
```

