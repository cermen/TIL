# 장고 Admin

#### 슈퍼 유저 생성 

- `python manage.py createsuperuser`

#### Admin에 모델 등록하기

`admin.site.register(model)`

````python
from django.contrib import admin
from .models import Question

admin.site.register(Question)
````

#### ModelAdmin

- 검색 기능 추가

```python
from django.contrib import admin
from .models import Question

class QuestionAdmin(admin.ModelAdmin):
    search_fields = ['subject']

admin.site.register(Question, QuestionAdmin)
```



