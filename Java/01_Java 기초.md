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

| 자료형  | 바이트 | 범위                                      |
| ------- | ------ | ----------------------------------------- |
| `short` | 2      | -32768\~32767 (-2^15\~2^15-1)             |
| `int`   | 4      | -2147483678\~2147483677 (-2^31\~2^31-1)   |
| `long`  | 8      | -9.22^10\*18\~9.22^10\*18 (-2^63\~2^63-1) |

**실수 자료형**

| 자료형   | 바이트 | 범위                                      |
| -------- | ------ | ----------------------------------------- |
| `float`  | 4      | (+/-)1.4E-45~(+/-)3.4028235E38            |
| `double` | 8      | (+/-)4.9E-324~(+/-)1.7976931348623157E308 |

- `float`의 경우에는 숫자 뒤에 `f`를 붙인다.

**문자 자료형**: `char`

- 문자를 담는 값

**논리 자료형**: `boolean`

- 참/거짓을 담는 값
- `True`와 `False`로만 나타낸다.

**바이트 자료형**: `byte`

- 바이트를 변수로 선언하며, 출력 시 아스키 코드 값을 반환한다.

**각 자료형 변수 선언 예시**

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

### 배열

- 참조 자료형: 자바의 인스턴스를 가리킬 수 있는 자료형
- **배열**:  동일한 자료형의 데이터를 연속된 공간에 저장하기 위한 자료구조
  - `자료형[] 배열이름 = new 지료형[크기]`와 같은 형태로 선언한다.
  - 인덱스는 0에서 (배열의 크기 - 1)까지의 값을 가진다.

**배열 선언 예시**

```java
int[] intEmptyArray = new int[5];
System.out.println(Arrays.toString(intEmptyArray));

int[] intArray = new int[] {1, 2, 3, 4, 5};
System.out.println(Arrays.toString(intArray));

String[] stringEmptyArray = new String[5];
System.out.println(Arrays.toString(stringEmptyArray));

String[] season = {"spring", "summer", "autumn", "winter"};
System.out.println(Arrays.toString(season));

System.out.println(season.length);
System.out.println(season[season.length - 1]);
```

### 연산자

**산술 연산자**: `+`, `-`, `*`, `/`, `%`

```java
int num1 = 10;
int num2 = 5; 

System.out.println(num1 + num2); // 더하기 연산
System.out.println(num1 - num2); // 빼기 연산
System.out.println(num1 * num2); // 곱하기 연산
System.out.println(num1 / num2); // 나누기 연산
System.out.println(num1 % num2); // 나머지 연산
```

**대입 연산자**: 연산자 앞에 `=`을 붙인다.

```java
num1 += num2; // num1 = num1 + num2
System.out.println(num1);

num1 -= num2; // num1 = num1 - num2
System.out.println(num1);

num1 *= num2; // num1 = num1 * num2
System.out.println(num1);

num1 /= num2; // num1 = num1 / num2
System.out.println(num1);

num1 %= num2; // num1 = num1 % num2 
System.out.println(num1);
```

**관계 연산자**

- `==` : 두 값이 같은지, `!=` : 두 값이 같지 않은지
- `>` : 왼쪽이 오른쪽보다 큰지, `>=` : 왼쪽이 오른쪽보다 크거나 같은지
- `<` : 왼쪽이 오른쪽보다 작은지, `<=` : 왼쪽이 오른쪽보다 작거나 같은지
- 참이면 `true`를, 거짓이면 `false`를 반환한다.

```java
int num1 = 10;
int num2 = 20;
int num3 = 10;

System.out.println(num1 > num2); // 10 > 20
System.out.println(num1 >= num3); // 10 >= 10
System.out.println(num1 < num2); // 10 < 20
System.out.println(num1 <= num2); // 10 <= 20
System.out.println(num1 == num3); // 10 == 10
System.out.println(num1 != num2); // 10 != 20
```

**논리 연산자**

- `&&` : 두 가지 모두 참일 때 true를, 그렇지 않을 경우 false를 반환한다.
- `||` : 두 가지 하나라도 참일 때 true를, 그렇지 않을(둘 다 거짓일) 경우 false를 반환한다.
- `!` : 피연산자의 논리값을 바꾼다.

```java
int num1 = 10;
int num2 = 20;

System.out.println(a && b);		// false
System.out.println(a || b);		// true
System.out.println(!b);			// true
```

**비트 연산자**

피연산자를 비트 단위로 논리 연산한다.

- `&` : AND - 대응되는 비트가 모두 1이면 1을 반환함. 
- `|` : OR - 대응되는 비트 중에서 하나라도 1이면 1을 반환함.
- `^` : XOR - 대응되는 비트가 서로 다르면 1을 반환함.
- `~` : NOT - 비트를 1이면 0으로, 0이면 1로 반전시킴.
- `<<` - 지정한 수만큼 비트들을 전부 왼쪽으로 이동시킴.
- `>>` - 부호를 유지하면서 지정한 수만큼 비트를 전부 오른쪽으로 이동시킴.

```java
int num1 = 5;	// 0101
int num2 = 9;	// 1001

System.out.println(num1 & num2);	// 1  (0001)
System.out.println(num1 | num2)		// 13 (1101)
System.out.println(~num1);			// -6 (..111010)
```



