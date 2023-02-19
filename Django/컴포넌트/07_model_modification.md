# 모델 변경

### author 속성 추가

1. Question 모델에 author 속성을 추가한다.

   ```python
   from django.db import models
   from django.contrib.auth.models import User # 추가
   
   
   class Question(models.Model):
       author = models.ForeignKey(User, on_delete=models.CASCADE)
       # 이하 생략
   
   
   class Answer(models.Model):
       author = models.ForeignKey(User, on_delete=models.CASCADE)
       # 이하 생략
   ```

2. makemigrations 명령어를 입력해 데이터베이스를 변경한다.

3. option을 선택하라는 메시지가 뜸
   
4. migrate 명령어로 변경된 DB를 적용한다.

### author 저장

```python
# pybo\views.py
def answer_create(request, question_id):
    # 생략
        if form.is_valid():
            answer = form.save(commit=False)
            answer.author = request.user  # author 속성에 로그인 계정 저장
	# 생략

def question_create(request, question_id):
    # 생략
        if form.is_valid():
            answer = form.save(commit=False)
            answer.author = request.user  # author 속성에 로그인 계정 저장
	# 생략       
```

### 로그인이 필요한 함수

로그아웃 상태에서 질문 또는 답변을 등록하면 ValueError가 발생 => User가 아닌 AnonymousUser가 대입되어 발생

=> 이를 해결하기 위해 `@login_required` 애너테이션을 사용한다.

```python
# pybo\views.py
from django.shortcuts import render, get_object_or_404, redirect
from .models import Question
from django.utils import timezone
from .forms import QuestionForm, AnswerForm
from django.core.paginator import Paginator
from django.contrib.auth.decorators import login_required

# 생략

@login_required(login_url='common:login')
def answer_create(request, question_id):
    # 생략


@login_required(login_url='common:login')
def question_create(request):
	# 생략
```

### next

로그아웃 상태에서 질문 등록하기를 눌러 로그인 화면으로 전환된 상태의 URL을 보면 next 파라미터가 나타난다. => 로그인 성공 후 next 옆에 있는 URL로 이동할 것을 의미한다. 

xxxxxxxxxx {% extends 'base.html' %}{% load pybo_filter %}{% block content %}<div class="container my-3">    <table class="table">        <thead>            <tr class="thead-dark">                <th>번호</th>                <th>제목</th>                <th>작성일시</th>            </tr>        </thead>        <tbody>            {% if question_list %}            {% for question in question_list %}            <tr>                <td>                    <!-- 번호 = 전체건수 - 시작인덱스 - 현재인덱스 + 1 -->                    {{ question_list.paginator.count|sub:question_list.start_index|sub:forloop.counter0|add:1 }}                </td>                <td><a href="{% url 'pybo:detail' question.id %}">{{ question.subject }}</a></td>                <td>{{ question.create_date }}</td>            </tr>html

```html
<!--templates\common\login.html  -->
<form method="POST" class="post-form" action="{% url 'common:login' %}">
    {% csrf_token %}
    <input type="hidden" name="text" value="{{ next }}">  <!-- 로그인 성공 후 이동되는 URL -->
    {% include "form_errors.html" %}
```

### disabled

비로그인 상태에서 댓글을 작성하는 것을 막기 위해 disabled 속성을 추가한다.

```html
<!-- templates\pybo\question_detail.html -->
<div class="form-group">
    <textarea {% if not user.is_authenticated %}disabled{% endif %}
    name="content" id="content" class="form-control" rows="10"></textarea>
</div>
<input type="submit" value="답변등록" class="btn btn-primary">
```

