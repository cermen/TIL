# 파이썬 입문

### 파이썬의 특징

- **장점**
  - 상대적으로 쉽다
  - interactive programming
  - 분석, 통계에 관련된 library 풍부하다
  - Open Source(무료)
  - R에 비해서 범용적

- **단점**
  - 하위호환성이 없다 (버전 2에서 쓰는 것이 3에서는 사용 안 됨)

### 변수의 생성 및 삭제
- 파이썬은 인터프리터 기반의 언어
- 변수 맨 앞에 숫자 사용할 수 없음, 특수문자는 _와 $
- 변수 선언 방법
  - camelCase : 함수 정의 시 많이 사용하는 방법
  - PascalCase : 클래스 정의 시 많이 사용하는 방법
  - snake_case

- 예약어는 변수명으로 사용 불가

### print 함수
- 한 문장을 출력하는 함수
- `sep` 옵션 : 각 단어를 이어주는 글자 지정
- `end` 옵션 : 문장의 끝 글자를 지정
  - 기본값은 `\n`(줄바꿈)
  - `''` 혹은 `' '`일 경우 줄바꿈 안함
- format
  ```python
  one = 'one'
  two = 'two'
  
  print("%s %s" % (one, two))
  print("{} {}".format(one, two))
  print("{1} {0}".format(one, two))
  
  print('%10s' % ('nice'))
  print('%-10s' % ('nice'))
  print('%10.5f' % 3.1415926535)
  print('{:10.5f}'.format(3.1415926535))
  ```
  ```
  -- 출력 결과 --
  one two
  one two
  two one
        nice
  nice      
     3.14159
     3.14159
  ```
