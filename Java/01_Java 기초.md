# Java 기초

### Java 개요

- 썬 마이크로시스템즈에서 1995년에 개발한 객체지향 프로그래밍 언어
- 웹 개발, 모바일 앱 개발 등에 널리 사용되고 있다.

#### Java 기초 코드

```java
public class HelloWorld {
	public static void main(String[] args) {
		System.out.println("Hello world!");
	}
}
```

### 표준 입력과 출력

- 표준 출력에는 `System.out.println()`을 사용한다.
- 표준 입력에는 `Scanner` 객체를 이용한다. 
  특정 변수에 값을 대입하는 데 `next()` 계열의 메서드를 사용하며, 변수 자료형마다 서로 다르다.
  - `nextInt()` : Integer형 변수에 값 대입
  - `nextFloat()` : Float형 변수에 값 대입
  - `nextDouble()` : Double형 변수에 값 대입
  - `next()` : String형 단어 값 대입
  - `nextLine()` : String형 문장 값 대입

```java
Scanner scanner = new Scanner(System.in);
String myString = scanner.next();	// String형 단어 값 대입
int myInt = scanner.nextInt();		// Integer형 변수에 값 대입
scanner.close();

System.out.println("myString is: " + myString);
System.out.println("myInt is: " + myInt);
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

### 조건문

#### if문

아래의 형식을 가지며 조건식이 true일 경우에 실행 코드가 구현된다.

```java
if (조건식){
    실행 코드
}
```

**예시**

```java
int check = 100;
int num1 = 150;
if (num1 > check) {
    System.out.println("100보다 큰 수입니다");
}
```

```java
int num2 = 50;
if (num1 > check) {
    System.out.println("100보다 큰 수입니다");
} else {
    System.out.println("100보다 작은 수입니다.");
}
```

#### switch문

입력 변수에 따라 해당 변수에 해당하는 경우의 로직을 수행한다.

```java
char score = 'A';
switch (score) {
    case 'A':
        System.out.println("A등급입니다.");
        break;
    case 'B':
        System.out.println("B등급입니다.");
        break;
    case 'C':
        System.out.println("C등급입니다.");
        break;
    default:
        System.out.println("C등급보다 낮은 등급입니다.");
        break;
}
```

- **주의**: `break`를 하지 않을 경우 다음 case 코드 블럭도 실행된다.

#### 삼항연산자

> `(조건식) ? A : B`

조건식이 참일 경우 왼쪽 로직을, 거짓일 경우 오른쪽 로직을 수행한다.

```java
int a = 5;

String result = (a < 10) ? "10보다 작습니다." : "10보다 큽니다.";
System.out.println(result);		// "10보다 작습니다." 출력
```

### 반복문

#### while문

조건식을 더이상 만족하지 않을 때까지 괄호 안의 로직을 반복 수행한다.

```
while (조건식){
    실행 코드 블럭
}
```

```java
int i = 0;
int sum = 0;
while (i < 10) {
    sum += i + 1;
    i += 1;
}
System.out.println(sum);
```

#### for문

```java
for(초기값 ; 조건식 ; 증감식){
    실행 코드 블럭
}
```

**예시**

```javascript
int sum = 0;

for (int i = 0; i < 10; i++) {
    sum += (i + 1);
}
System.out.println(sum);
```

#### for-each문

- Python의 for-in문과 동일한 기능을 한다.

```java
for (String day : days) {
    System.out.println(day);
}
```

#### do-while문

기존 while문의 조건 검사를 끝 부분(로직 수행 후)에 수행한다.

```java
int i = 1;
int result = 0;
do {
    result += i;
    i += 1;
} while (i < 2);
System.out.println(result);
```

#### break와 continue

- `break`: if문 내의 로직에 해당할 경우 반복문 실행을 중단한다.

```java
int i = 0;
while (i < 10){
    if (i==5){
        break;
    }
    i += 1;
}
System.out.println(i);	// 5
```

- `continue` : if문 내의 로직에 해당할 경우 해당 회차(iteration)의 이후 로직을 생략한다.

```java
// 숫자 0~9 중 5를 제외하고 모두 출력된다.
for(int i=0;i<10;i++){
    if (i==5){
        continue;
    }
    System.out.println(i);
}
```

