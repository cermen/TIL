# 수정과 삭제

### 수정 시각 추가

```python
class Question(models.Model):
    # 생략
    modify_date = models.DateTimeField(null=True, blank=True)
    # 생략

class Answer(models.Model):
    # 생략
    modify_date = models.DateTimeField(null=True, blank=True)
```

모델을 위와 같이 변경한 후에 makemigrations, migrate를 수행한다.

### urls.py에 매핑 규칙 추가

```python
urlpatterns = [
    (... 생략 ...)
    path('question/modify/<int:question_id>/', views.question_modify, name='question_modify'),	# 질문 수정
    path('question/delete/<int:question_id>/', views.question_delete, name='question_delete'),	# 질문 삭제
    path('answer/modify/<int:answer_id>/', views.answer_modify, name='answer_modify'),			# 답변 수정
    path('answer/delete/<int:answer_id>/', views.answer_delete, name='answer_delete'),			# 답변 삭제
]
```



### 질문 수정

##### question_detail.html에 질문 수정 버튼 추가

```html
<!-- 질문 -->
<h2 class="border-bottom py-2">{{ question.subject }}</h2>
<div class="card my-3">
    <div class="card-body">
        <div class="card-text" style="white-space: pre-line;">{{ question.content }}</div>
        <div class="d-flex justify-content-end">
            <div class="badge bg-light text-dark p-2 text-start">
                <div class="mb-2">{{ question.author.username }}</div>
                <div>{{ question.create_date }}</div>
            </div>
        </div>
        <div class="my-3">
            {% if request.user == question.author %}
            <a href="{% url 'pybo:question_modify' question.id  %}" 
               class="btn btn-sm btn-outline-secondary">수정</a>
            {% endif %}
        </div>
    </div>
</div>
```

##### urls.py에 path 추가

```python
urlpatterns = [
    # 생략
    path('question/modify/<int:question_id>/', views.question_modify, name='question_modify'),
]
```

##### views.py에 질문 수정 로직 추가

```python
# import 추가
from django.contrib import messages

@login_required(login_url='common:login')
def question_modify(request, question_id):
    question = get_object_or_404(Question, pk=question_id)
    if request.user != question.author:
        messages.error(request, '수정권한이 없습니다')
        return redirect('pybo:detail', question_id=question.id)
    if request.method == "POST":
        form = QuestionForm(request.POST, instance=question)
        if form.is_valid():
            question = form.save(commit=False)
            question.modify_date = timezone.now()  # 수정일시 저장
            question.save()
            return redirect('pybo:detail', question_id=question.id)
    else:
        form = QuestionForm(instance=question)
    context = {'form': form}
    return render(request, 'pybo/question_form.html', context)
```

### 질문 삭제

##### question_detail.html에 질문 삭제 버튼 추가

```html
<div class="my-3">
    {% if request.user == question.author %}
    <a href="{% url 'pybo:question_modify' question.id  %}"
       class="btn btn-sm btn-outline-secondary">수정</a>
    <a href="javascript:void(0)" class="delete btn btn-sm btn-outline-secondary"
       data-uri="{% url 'pybo:question_delete' question.id  %}">삭제</a>
    {% endif %}
</div>
```

- `javascript:void(0)` - 해당 링크를 클릭해도 아무 동작도 하지 않는다.
- `data-uri` 속성: 자바스크립트에서 클릭 이벤트 발생시 `this.dataset.uri`와 같이 사용하여 그 값을 얻을 수 있다.

##### views.py에 질문 삭제 로직 추가

```python
@login_required(login_url='common:login')
def question_delete(request, question_id):
    question = get_object_or_404(Question, pk=question_id)
    if request.user != question.author:
        messages.error(request, '삭제권한이 없습니다')
        return redirect('pybo:detail', question_id=question.id)
    question.delete()
    return redirect('pybo:index')
```

### 답변 수정

##### question_detail.html에 답변 수정 버튼 추가

```html
<h5 class="border-bottom my-3 py-2">{{question.answer_set.count}}개의 답변이 있습니다.</h5>
{% for answer in question.answer_set.all %}
<div class="card my-3">
    <div class="card-body">
        <div class="card-text" style="white-space: pre-line;">{{ answer.content }}</div>
        <div class="d-flex justify-content-end">
            <div class="badge bg-light text-dark p-2 text-start">
                <div class="mb-2">{{ answer.author.username }}</div>
                <div>{{ answer.create_date }}</div>
            </div>
        </div>
        <div class="my-3">
            {% if request.user == answer.author %}
            <a href="{% url 'pybo:answer_modify' answer.id  %}" 
               class="btn btn-sm btn-outline-secondary">수정</a>
            {% endif %}
        </div>
    </div>
</div>
{% endfor %}
```

##### views.py에 답변 수정 로직 추가

```python
from .models import Question, Answer	# Answer 모델 추가


@login_required(login_url='common:login')
def answer_modify(request, answer_id):
    answer = get_object_or_404(Answer, pk=answer_id)
    if request.user != answer.author:
        messages.error(request, '수정권한이 없습니다')
        return redirect('pybo:detail', question_id=answer.question.id)
    if request.method == "POST":
        form = AnswerForm(request.POST, instance=answer)
        if form.is_valid():
            answer = form.save(commit=False)
            answer.modify_date = timezone.now()
            answer.save()
            return redirect('pybo:detail', question_id=answer.question.id)
    else:
        form = AnswerForm(instance=answer)
    context = {'answer': answer, 'form': form}
    return render(request, 'pybo/answer_form.html', context)
```

#### 답변 수정 폼

답변 수정을 위한 템플릿으로 answer_form.html을 추가한다.

```html
{% extends 'base.html' %}
{% block content %}
<!-- 답변 수정-->
<div class="container my-3">
    <form method="post">
        {% csrf_token %}
        {% include "form_errors.html" %}
        <div class="mb-3">
            <label for="content" class="form-label">답변내용</label>
            <textarea class="form-control" name="content" id="content"
                      rows="10">{{ form.content.value|default_if_none:'' }}</textarea>
        </div>
        <button type="submit" class="btn btn-primary">저장하기</button>
    </form>
</div>
{% endblock %}
```

### 답변 삭제

##### question_detail.html에 답변 삭 버튼 추가

```html
<h5 class="border-bottom my-3 py-2">{{question.answer_set.count}}개의 답변이 있습니다.</h5>
{% for answer in question.answer_set.all %}
<div class="card my-3">
    <div class="card-body">
        (... 생략 ...)
        <div class="my-3">
            {% if request.user == answer.author %}
            <a href="{% url 'pybo:answer_modify' answer.id  %}"
               class="btn btn-sm btn-outline-secondary">수정</a>
            <a href="#" class="delete btn btn-sm btn-outline-secondary "
               data-uri="{% url 'pybo:answer_delete' answer.id  %}">삭제</a>
            {% endif %}
        </div>
    </div>
</div>
```

##### views.py에 답변 수정 로직 추가

```python
@login_required(login_url='common:login')
def answer_delete(request, answer_id):
    answer = get_object_or_404(Answer, pk=answer_id)
    if request.user != answer.author:
        messages.error(request, '삭제권한이 없습니다')
    else:
        answer.delete()
    return redirect('pybo:detail', question_id=answer.question.id)
```

#### 
