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

  