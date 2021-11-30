# 로그인과 로그아웃

로그인, 로그아웃 기능 구현하는 앱 : `django.contrib.auth`

### common 앱

하나의 웹 사이트에는 게시판만 아니라 블로그, 쇼핑몰 등 여러 거지 앱이 있을 수 있기 때문에 모든 앱에서 공통으로 사용되는 기능인 로그인, 로그아웃 기능을 하나의 앱에 종속시키는 것은 옳지 않다. => 공통으로 사용되는 기능은 common 앱에 넣는다.

1. common 앱 생성 => `django-admin startapp common`
2. `config\settings.py` 파일에 common 앱을 등록한다.
3. `config\urls.py` 파일에 `path('common/', include('common.urls'))`를 추가한다.
4. `common\urls.py` 파일을 생성한다.

### 로그인

templates\common 디렉터리에 `login.html` 템플릿을 생성한다.

```html
{% extends "base.html" %}
{% block content %}
<div class="contaier my-3">
    <form method="POST" class="post-form" action="{% url 'common:login' %}">
        {% csrf_token %}
        {% include "form_errors.html" %}
        <div class="form-group">
            <label for="username">사용자ID</label>
            <input type="text" class="form-control" name="username" id="username"
                value="{{ form.username.value|default_if_none:'' }}">
        </div>
        <div class="form-group">
            <label for="password">비밀번호</label>
            <input type="password" class="form-control" name="password" id="password"
                value="{{ form.password.value|default_if_none:'' }}">
        </div>
        <button type="submit" class="btn btn-primary">로그인</button>
    </form>
</div>
{% endblock %}
```

- `templates\form_errors.html`

```html
{% if form.errors %}
{% for field in form %}
{% for error in field.errors %}  <!-- 필드 오류를 출력한다. -->
<div class="alert alert-danger">
    <strong>{{ field.label }}</strong>
    {{ error }}
</div>
{% endfor %}
{% endfor %}
{% for error in form.non_field_errors %}  <!-- 넌필드 오류를 출력한다. -->
<div class="alert alert-danger">
    <strong>{{ error }}</strong>
</div>
{% endfor %}
{% endif %}
```