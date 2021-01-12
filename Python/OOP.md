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
    raise_rate = 1.1    # 급여인상률(class 변수)
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



## 객체지향의 주요 개념

### 상속 (Inheritance)

- 기존 클래스를 추가하여 멤버 추가하거나 동작 변경
```python
class Parent(object):
    # 파이썬에서는 다른 언어와는 달리 생성자를 한 번밖에 쓸 수 없다.
    def __init__(self, name, job):
        self.name = name
        self.job = job

class Child(Parent):	# Parent 클래스를 상속
    def __init__(self, name, job, age):
        super().__init__(name, job)	# super() : 부모 클래스를 지칭함
        self.age = age
```

### 은닉화 (Encapsulation, 캡슐화)

- 객체의 데이터와 기능을 하나로 묶고 외부에 노출되지 않도록 숨김 처리 하는 것
- 파이썬은 protected, private 등의 접근 제어자가 없음
  - 변수/함수명 앞에 `_`를 붙이면 protected가 되며, `__`를 붙이면 private가 된다.

```python
class HidingClass(object):
    def __init__(self, name, dept, num):
        self.utype = self.__class__.__name__
        self.name = name
        self.__dept = dept	# __로 시작하는 변수는 외부에서 접근이 되지 않는다.
        self.num = num

    # private 변수에 접근하기 위해서는 getter와 setter 함수를 이용
    def get_dept(self):
        return self.__dept
    
    def set_dept(self, dept):
        self.__dept = dept

    def __info(self):
        return "__로 시작했기 때문에 해당 함수는 외부에서 접근이 되지 않습니다."
```

### 다형성 (Polymorphism)

- 상위 클래스에 정의된 함수를 하위 클래스에서 해당 함수를 재정의(method overriding)
```python
class Animal:
    def __init__(self, name):
        self.name = name
    
    def hello(self):
        print(self.name, '안녕')

class Dog(Animal):
    def hello(self):
        print(self.name, '멍멍')
        
class Duck(Animal):
    def hello(self):
        print(self.name, '꽥꽥')

animal = Animal('돌이')
dog = Dog('바둑이')
duck = Duck('오리')
animal.hello()
dog.hello()
duck.hello()
```

```
--- 실행 결과 ---
돌이 안녕
바둑이 멍멍
오리 꽥꽥
```

### 추상 클래스 (Abstraction Class)

- 메서드 구현을 강제하기 위해 사용
- 추상 메서드(함수)를 하나라도 가지면 추상 클래스가 된다.
- 추상 클래스는 객체를 생성하지 않는다.
- 추상 클래스를 구현하려면 `abc` 모듈을 import해야 한다.
```python
from abc import *

class Base(metaclass=ABCMeta):
    @abstractmethod
    def study(self):
        pass

    def go_to_school(self):
        print('학교에 갑니다.')

class Student(Base):
    def study(self):
        print('공부하자~')
        
# obj = Base() - 오류
# obj.go_to_school()

stu = Student()
stu.go_to_school()
stu.study()
```
```
--- 실행 결과 ---
학교에 갑니다.
공부하자~
```
### 다중 상속

- 두 개 이상의 클래스의 속성을 물려받는 것

```python
class Animal(object):
    def cry(self):
        pass

class Lion(Animal):
    def bite(self):
        print('한 입에 꿀꺽한다')

    def cry(self):
        print('그르렁')

class Tiger(Animal):
    def jump(self):
        print('호랑이가 점프를 한다')

    def cry(self):
        print('어흥')

class Liger(Lion, Tiger):
    def play(self):
        print('라이거가 사육사와 재미있게 놀고 있다.')
        
liger = Liger()
liger.play()
liger.cry() # 다중상속된 클래스의 메서드의 경우 먼저 정의된 부모 클래스의 메서드가 실행된다.
```

```
--- 실행 결과 ---
라이거가 사육사와 재미있게 놀고 있다.
그르렁
```

