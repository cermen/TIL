# 웹페이지를 파이썬 Flask로 만들기

## Jinja2 템플릿

- 웹페이지에 필요한 부분을 변경할 필요가 있을 때 사용하는 간단한 문법

```
{{ 변수명 }}

{% 파이썬 소스코드 %}
```

 ### 반복문

- `for`로 선언하고, `endfor`로 끝난다.
  `{% for %}`, `{% endfor %}`

- 들여쓰기(indentation)는 안 해도 됨.

```
{% for value in values %}
{{ value }}
{% endfor %}
```


### 조건문

- `if`, `elif`, `else`, `endif`로 구성
  `{% if %}`, `{% elif %}`, `{% else %}`, `{% endif %}`
- `elif`, `else`는 조건에 따라 안 써도 됨

### 주석

`{# #}`으로 표시한다.

```html
{% if age >= 60 %}
<h3>60대 이상입니다.</h3>
{% elif age >= 50 %}
<h3>50대입니다.</h3>
{% elif age >= 40 %}
<h3>40대입니다.</h3>
{% elif age >= 30 %}
<h3>30대입니다.</h3>
{% elif age >= 20 %}
<h3>20대입니다.</h3>
{#}
{% else %}
<h3>미성년자입니다.</h3>
#}
{% endif %}
```

