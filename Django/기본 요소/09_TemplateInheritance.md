# 템플릿 상속

### 표준 HTML 구조

- 표준 HTML 문서는 html, head, body 엘리먼트가 있어야 하며, CSS 파일은 head 엘리먼트 안에 있어야 한다. 또한 head 엘리먼트 안에는 meta, title 엘리먼트 등이 포함되어야 한다.

### 템플릿 상속

- CSS 파일 이름이 변경되거나 새로운 CSS 파일이 추가될 때마다 모든 템플릿 파일을 일일이 수정해야 한다.
- 이를 해소하기 위해 템플릿 상속 기능을 제공한다.

```html
<!-- templates/base.html : 기본 템플릿 -->
{% load static %}
<!DOCTYPE html>
<html lang="ko">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <link rel="stylesheet" type="text/css" href="{% static 'bootstrap.min.css' %}">
    <link rel="stylesheet" type="text/css" href="{% static 'style.css' %}">
    <title>Hello, pybo!</title>
</head>

<body>
<!-- 기본 템플릿 안에 삽입될 내용 Start -->
{% block content %}
{% endblock %}  
<!-- 기본 템플릿 안에 삽입될 내용 End -->
</body>
</html>
```

- 위 파일을 다음과 같이 적용한다.

```html
{% extends 'base.html' %}
{% block content %}
<!-- 내용 -->
<!-- 내용 -->
{% endblock %}
```

