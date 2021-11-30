# 템플릿

#### render() 함수

- 모델 데이터를 화면에 출력하는 함수
- `render(request, 띄울 템플릿 파일, context)`

```python
# pybo/views.py
def index(request):
    question_list = Question.objects.order_by('-create_date')
    context = {'question_list': question_list}
    return render(request, 'pybo/question_list.html', context)
```

#### 템플릿을 저장할 디렉터리를 만들고 등록하기

명령 프롬프트에서 `mkdir templates`를 입력하거나 파이참에서 프로젝트 폴더 아래에 template 폴더를 생성한 후 `config/settings.py`에 등록한다.

````python
# config/settings.py
TEMPLATES = [
    {
    	# ------------- 생략 -------------
        'DIRS': [BASE_DIR / 'templates'],
        # ------------- 생략 -------------
    },
]
````

#### 템플릿 파일 만들기

```html
<!-- templates/pybo/question_detail.html -->
<body>
    {% if question_list %}
    <ul>
        {% for question in question_list %}
        <li><a href="/pybo/{{ question.id }}/">{{ question.subject }}</a></li>
        {% endfor %}
    </ul>
    {% else %}
    <p>질문이 없습니다.</p>
    {% endif %}
</body>
```

##### 템플릿 태그

- `{% if list %}` : list가 있다면
  - `{% elif 조건문 %}` : 아닌 것들 중에서 조건문에 맞으면
  - `{% else %}` : 아니라면
  - `{% endif %}` : `if` 구문의 끝
- `{% for item in list %}` : list를 반복하며 순차적으로 item에 대입
  - `{% endfor %}` : `for` 구문의 끝
- `{{ item.id }}` : for 문에 의해 대입된 item 객체의 id 출력 

#### pybo/urls.py에 URL 매핑 추가하기

현재까지의 상태에서 질문 항목을 누르면 404 오류가 뜬다.
→ 질문 항목에 대한 URL 매핑을 추가해야 한다.

```python
# pybo/urls.py
from django.urls import path

from . import views

app_name = 'pybo'

urlpatterns = [
    path('', views.index, name='index'),
    # URL 매핑
    path('<int:question_id>/', views.detail)
]
```

#### pybo/views.py에 화면 추가하기

```python
# pybo/views.py
def detail(request, question_id):
    # pybo 내용 출력
    question = Question.objects.get(id=question_id)
    context = {'question': question}
    return render(request, 'pybo/question_detail.html', context)
```

```html
<!-- templates/pybo/question_detail.html -->
<body>
    <h1>{{ question.subject }}</h1>

    <div>
        {{ question.content }}
    </div>
</body>
```

#### 오류 화면 구현하기

```python
# pybo/views.py
from django.shortcuts import render, get_object_or_404
from .models import Question

def detail(request, question_id):
    question = get_object_or_404(Question, pk=question_id)
    context = {'question': question}
    return render(request, 'pybo/question_detail.html', context)
```

- `get_object_or_404(model, pk=)` : pk에 해당하는 건이 없으면 오류 대신 404 페이지를 반환한다.