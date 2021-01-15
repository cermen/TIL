# 파일 입출력

#### open 함수
```python
open(파일경로, 모드)
```

- 모드
  - `r` : 파일 읽기 (파일이 없을 시 예외 발생)
  - `w` : 파일 쓰기 (파일이 이미 있으면 덮어쓴다.)
  - `a` : 파일에 데이터 추가
  
- 예시

  ```python
  # 'Hi, Wook'을 hello.txt에 쓴다.
  file = open(file='hello.txt', mode='w')
  file.write('Hi, Wook')
  file.close()		# 작업이 끝나면 close() 함수를 실행해야 한다.
  
  # hello.txt를 읽어들여 내용을 출력한다.
  file = open(file='hello.txt', mode='r')
  print(file.read())
  file.close()
  
  # hello.txt에 '\nNice to meet you!'를 추가한다.
  file = open(file='hello.txt', mode='a')
  file.write('\nNice to meet you!')
  file.close()
  ```
#### with-as 구문

`close()` 함수를 출력할 필요 없이 파일을 열고 닫을 수 있다.

```python
with open(file='hello.txt', mode='r') as file:
    print(file.read())
```

