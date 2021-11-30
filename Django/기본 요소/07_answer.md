# 답변 등록 기능 만들기

#### 답변 등록 버튼 만들기

```html
<!-- templates/pybo/question_detail.html -->
<body>
    <!-- 생략 -->
    
    <form action="{% url 'pybo:answer_create' question.id %}" method="post">
        {% csrf_token %}
        <textarea name="content" id="content" rows="15"></textarea>
        <input type="submit" value="답변등록">
    </form>
</body>
```

`{% csrf_token %}` : CSRF 공격을 방지하기 위해 넣는 태그

- CSRF 공격 : Cross-Site Request Forgery - 사이트 간 요청 위조 공격

#### URL 매핑 등록하기

```python
# pybo/urls.py

urlpatterns = [
    path('', views.index, name='index'),
    path('<int:question_id>/', views.detail, name='detail'),
    # 추가
    path('answer/create/<int:question_id>/', views.answer_create, name='answer_create')
]
```

#### answer_create 함수 추가하기

```python
# pybo/views.py

# redirect, timezone 추가
from django.shortcuts import render, get_object_or_404, redirect
from .models import Question
from django.utils import timezone

def answer_create(request, question_id):
    question = get_object_or_404(Question, pk=question_id)
    question.answer_set.create(content=request.POST.get('content'), create_date=timezone.now())
    return redirect('pybo:detail', question_id=question_id)
```

- `redirect(페이지, question_id=question_id)` : 함수에 전달된 값을 참고하여 페이지 이동을 수행

#### 등록된 답변 표시하기

```html
<body>
    <h1>{{ question.subject }}</h1>

    <div>
        {{ question.content }}
    </div>
    
    <!-- 추가 부분 -->
    <h5>{{ question.answer_set.count }}개의 답변이 있습니다.</h5>
    <div>
        <ul>
            {% for answer in question.answer_set.all %}
            <li>{{ answer.content }}</li>
            {% endfor %}
        </ul>
    </div>

    <form action="{% url 'pybo:answer_create' question.id %}" method="post">
        {% csrf_token %}
        <textarea name="content" id="content" rows="15"></textarea>
        <input type="submit" value="답변등록">
    </form>
</body>
```

