# 템플릿 필터

페이지를 이동해도 게시물 번호가 1부터 시작함 => 이 문제점을 해결하기 위해 템플릿 필터를 사용함

- templatetags 디렉터리를 생성하고 그 안에 pybo_filter.py 파일을 생성하여 템플릿 필터 함수를 만든다.

```python
from django import template

register = template.Library()

@register.filter
def sub(value, arg):
    return value - arg
```

- 템플릿 필터를 적용한 `templates\pybo\question_list.html` 파일

```html
{% extends 'base.html' %}
{% load pybo_filter %}
{% block content %}
<div class="container my-3">
    <table class="table">
        <thead>
            <tr class="thead-dark">
                <th>번호</th>
                <th>제목</th>
                <th>작성일시</th>
            </tr>
        </thead>
        <tbody>
            {% if question_list %}
            {% for question in question_list %}
            <tr>
                <td>
                    <!-- 번호 = 전체건수 - 시작인덱스 - 현재인덱스 + 1 -->
                    {{ question_list.paginator.count|sub:question_list.start_index|sub:forloop.counter0|add:1 }}
                </td>
                <td><a href="{% url 'pybo:detail' question.id %}">{{ question.subject }}</a></td>
                <td>{{ question.create_date }}</td>
            </tr>
```