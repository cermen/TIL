# Java 기초

### Java 개요

- 썬 마이크로시스템즈에서 1995년에 개발한 객체지향 프로그래밍 언어
- 웹 개발, 모바일 앱 개발 등에 널리 사용되고 있다.

#### Java 기초 코드

```java
public class HelloWorldApp {
	public static void main(String[] args) {
		System.out.println("Hello world!");
	}
}
```

### 변수와 상수

- **변수**: 값을 변경할 수 있는 곳
  - `자료형 변수명`과 같은 형태로 사용한다.
- **상수**: 값을 변경할 수 없는 곳
  - 자료형 앞에 `final`을 붙인다.

```java
public class Main {
    public static void main(String[] args) {
        int number = 5;
        System.out.println(number);

        String sparta = "Hello Sparta";
        System.out.println(sparta);

        final int finalNumber = 1;      // final: 상수
        System.out.println(finalNumber);
        // finalNumber = 2;		// 상수의 값을 변경 시 오류가 발생한다.
    }
}
```

### 자료형

**정수 자료형**

| 자료형  | 바이트 | 범위                                    |
| ------- | ------ | --------------------------------------- |
| `short` | 2      | -32768~32767 (-2^15~2^15-1)             |
| `int`   | 4      | -2147483678~2147483677 (-2^31~2^31-1)   |
| `long`  | 8      | -9.22^10\*18~9.22^10\*18 (-2^63~2^63-1) |

**실수 자료형**

| 자료형   | 바이트 | 범위                                        |
| -------- | ------ | ------------------------------------------- |
| `float`  | 4      | (+/-)1.4E-45 ~ (+/-)3.4028235E38            |
| `double` | 8      | (+/-)4.9E-324 ~ (+/-)1.7976931348623157E308 |

- `float`의 경우에는 숫자 뒤에 `f`를 붙인다.

**문자 자료형**: `char`

- 문자를 담는 값

**논리 자료형**: `boolean`

- 참/거짓을 담는 값
- `True`와 `False`로만 나타낸다.

**바이트 자료형**: `byte`

- 바이트를 변수로 선언하며, 출력 시 아스키 코드 값을 반환한다.

```java
short s = 1;
int i = 2;
long l = 3;
float f = 4.4f;		// `float`의 경우에는 숫자 뒤에 `f`를 붙인다.
double d = 5.5;
char c = 'A';
boolean bool = true;
byte data = 'b';	// 'b'의 아스키 코드 값을 받는다.
```

