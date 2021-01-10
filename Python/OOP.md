# 객체지향 프로그래밍

- 프로그래밍을 객체의 관점에서 접근하는 패러다임
### 클래스와 객체

#### 클래스(Class)

- 여러 개의 함수와 데이터를 묶어서 객체를 생성할 수 있는 템플릿

- 구성 : 멤버 = 변수(데이터) + 메서드(함수) , 생성자(초기화)

#### 객체(Object)

- 클래스를 기반으로 생성된 것

#### 클래스 구현 예시

  ```python
class Calc:
    def __init__(self, x, y):	# 생성자 : 객체 생성 시 호출되는 함수
        self.x = x
        self.y = y

    def plus(self):				# 메서드 : 사용자 정의 함수, 인스턴스 소유
        print(self.x + self.y)

obj = Calc(2, 3)	# 객체 생성
obj.plus()
  ```

### 특수 메서드
- `__str__` : `str(객체)` 형식으로 객체를 문자열화한다.
- `__repr__` : `repr(객체)` 형식으로 객체의 표현식을 만든다.
- `__len__` : `len(객체)` 형식으로 객체의 길이를 조사한다.

### 클래스 변수와 클래스 메서드

#### 클래스 변수
- 한 클래스의 객체가  공통으로 사용하는 변수
- `클래스명.변수명`으로 나타냄
#### 클래스 메서드
- 한 클래스의 객체가  공통으로 사용하는 메서드
- 함수 위에 `@classmethod`를 붙여준다.
- 첫 번째 인수로 `cls`를 사용한다.
#### 정적 메서드
- 클래스에 포함되는 단순 유틸리티 메서드
- 특정 객체에 소속되거나 클래스 관련 동작하지 않음
- 함수 위에 `@staticmethod`를 붙여준다.
#### 예제
```python
class Employee:
    raise_rate = 1.1    # 급여인상률(class variavle)
    def __init__(self, name, salary):
        self.name = name
        self.salary = salary

    def get_salary(self):
        return '현재 {}님의 급여는 {}입니다.'.format(self.name, self.salary)

    # class 함수
    @classmethod
    def update_rate(cls, rate):
        cls.raise_rate = rate
        print('인상률이 {}로 변경되었습니다'.format(rate))

    def apply_raise(self):
        self.salary = int(self.salary * Employee.raise_rate)

    # static 함수
    @staticmethod
    def is_valid(salary):
        if salary < 0:
            print('급여는 음수가 될 수 없습니다.')

emp01 = Employee('jyu', 1000)

print('인상 전 급여 -', emp01.get_salary())

Employee.update_rate(1.5)
emp01.apply_raise()

print('인상 후 급여 -', emp01.get_salary())
```

```
--- 실행 결과 ---
인상 전 급여 - 현재 jyu님의 급여는 1000입니다.
인상률이 1.5로 변경되었습니다
인상 후 급여 - 현재 jyu님의 급여는 1500입니다.
```

