# 스태틱 & 부트스트랩

- 보기 좋은 화면을 만들기 위해 디자인을 적용하며, 이를 위해 스타일시트(CSS 파일)를 사용한다.

#### 스태틱 디렉토리 등록하기

```python
# settings.py
STATIC_URL = '/static/'
STATICFILES_DIRS = [
    BASE_DIR / 'static'
]
```

#### 템플릿에 스타일 적용

```html
{% load static %}
<link rel="stylesheet" type="text/css" href="{% static 'style.css' %}">
```

### 부트스트랩

- 프론트엔드 개발을 빠르고 쉽게 할 수 있는 프레임워크
  공식 홈페이지 : https://getbootstrap.com/
  Documentation : https://getbootstrap.com/docs/4.6/getting-started/introduction/

#### 부트스트랩 적용

```html
{% load static %}
<link rel="stylesheet" type="text/css" href="{% static 'bootstrap.min.css' %}">
```

