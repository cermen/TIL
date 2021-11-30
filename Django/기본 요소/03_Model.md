# 모델

**앱 생성 후 앱이 필요로 하는 모델을 만들어야 한다.**
-> `python manage.py migrate` 명령어

### 모델 만들기

#### 1. pybo/models.py에 모델 작성하기

```python
from django.db import models

class Question(models.Model):
    subject = models.CharField(max_length=200)
    content = models.TextField()
    create_date = models.DateTimeField()

class Answer(models.Model):
    question = models.ForeignKey(Question, on_delete=models.CASCADE)
    content = models.TextField()
    create_date = models.DateTimeField()
```

장고 모델의 속성들 : [docs.djangoproject.com/en/3.0/ref/models/fields/#field-types](https://docs.djangoproject.com/en/3.0/ref/models/fields/#field-types)

#### 2. config/settings.py에 pybo 앱 등록하기

settings.py의 `INSTALLED_APPS`에 `'pybo.apps.PyboConfig'`를 추가한다.
← 모델은 앱에 종속되어 있으므로 settings.py에 앱을 등록해야 테이블 작업을 진행할 수 있다.

#### 3. makemigrations로 테이블 작업 파일 생성하기

- 모델 구현 직후 `migrate` 명령을 실행하면 명령이 수행되지 않는다.
  ← 모델이 생성되거나 변경된 후 `migrate` 명령을 실행하려면 테이블 작업 파일이 필요하다.
- 테이블 작업 파일 생성 명령어 : `python manage.py makemigrations`

### 참고) 장고 쉘에서 모델 관리

- 모델 데이터 모두 조회  : `Model.objects.all()`
- 조건에 맞는 데이터 한 개 조회  : `Model.objects.get(조건)`
  - 조건에 맞지 않는 데이터 조회 시 오류 메시지 발생
- 조건에 맞는 데이터 여러 개 조회  : `Model.objects.filter(조건)`
  - 조건에 맞지 않는 데이터 조회 시 빈 QuerySet 반환

- 데이터 수정 : `save()`

  ```python
  q = Question.objects.get(id=2)
  q.subject = 'Django Model Question'
  q.save()
  ```

- 데이터 삭제 : `delete()`

  ```python
  q = Question.objects.get(id=1)
  q.delete()
  ```

- 연결된 데이터 조회하기 : `연결모델명_set()`

  ```python
  # Answer는 Question에 연결됨
  q = Question.objects.get(id=1)
  q.answer_set.all()
  ```

  