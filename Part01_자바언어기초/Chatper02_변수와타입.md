# 이것이 자바다 - Part01 - Chapter15 변수와 타입

## 목차
- [2.1 변수 선언](#21-변수-선언)
- [2.2 정수 타입](#22-정수-타입)
- [2.3 문자 타입](#23-문자-타입)
- [2.4 실수 타입](#24-실수-타입)
- [2.5 논리 타입](#25-논리-타입)
- [2.6 문자열 타입](#26-문자열-타입)
- [2.7 자동 타입 변환](#27-자동-타입-변환)
- [2.8 강제 타입 변환](#28-강제-타입-변환)
- [2.9 연산식에서 자동 타입 변환](#29-연산식에서-자동-타입-변환)

## `2.1 변수 선언`
- 변수 : 하나의 값을 저장할 수 있는 메모리 번지에 붙여진 이름
- 정수형 변수에는 정수만, 실수형 변수에는 실수만 저장할 수 있음
- 변수 이름은 첫 번째 글자가 문자여야하고, 중간부터는 문자, 숫자, $, _를 포함할 수 있다.
- 캐멀(camel) 스타일로 선언하는 것이 관례다. `(코드를 작성할 때 여러 단어를 혼합하여 명명하는 경우, 낙타 등처럼 대소문자가 섞여있도록 작성하는 스타일)`
  1. 자바 소스 파일명(클래스명)은 대문자로 시작하는 것이 관례, ex) Week.java, MemberGrade.java
  2. 변수 명은 소문자로 시작하는 것이 관례, ex) score, mathScore, sportsCar 
- 변수 선언은 저장되는 값의 타입과 이름만 결정한 것이지, 메모리에 할당된 것은 아니다. 변수에 최초로 값이 대입될 때 메모리에 할당되고, 해당 메모리에 저장된다.
- 변수에 최초로 값을 대입하는 행위를 변수 초기화라고 한다. 이때 값을 초기값이라고 한다.

## `2.2 정수 타입`

### Primitive Types
- 변수는 선언될 떄의 타입에 따라 저장할 수 있는 값의 종류와 허용 범위가 달라진다.
- 자바는 정수, 실수, 논리값을 저장할 수 있는 기본 타입 8개를 다음과 같이 제공

| 값의 분류 | 기본 타입 |
|:---:|:---:|
|정수|byte, char, short, int, long|
|실수|float, double|
|논리|boolean|

### 정수 타입
- 정수 타입은 총 5개이다.

| Type | 메모리 크기 | 저장되는 값의 허용 범위 ||
|:---:|:---:|:---:|:---:|
|`byte`|1byte (8bit)|-2^7 ~ (2^7-1)|-128 ~ 127|
|`short`|2byte (16bit)|-2^15 ~ (2^15-1)|-32,768 ~ 32,767|
|`char`|2byte (16bit)|0 ~ (2^16-1)|0 ~ 65535(유니코드)|
|`int`|4byte (32bit)|-2^31 ~ (2^31-1)|-2,147,483,648 ~ 2,147,483,647|
|`long`|8byte (64bit)|-2^63 ~ (2^63-1)|-9,222,372,036,854,775,808 ~ 9,222,372,036,854,775,807|

### 진수
- 2진수 : 0b 혹은 0B로 시작하고 0과 1로 작성
```java
int x = 0b1011;
int y = 0B10100;
```
- 8진수 : 0으로 시작하고 0~7 숫자로 작성
```java
int x = 013;
int y = 0206;
```
- 10진수 : 소수점이 없는 0~9 숫자로 작성
```java
int x = 12;
int y = 20;
```
- 16진수 : 0x 또는 0X로 시작하고 0~9, A ~ F 또는 a ~ f로 작성
```java
int x = 0xB3;
int y = 0Xffff;
```
> 코드에서 프로그래머가 직접 입력한 값을 `literal(리터럴)`이라고 부르는데, 변수에 대입할 정수 리터럴은 진수에 따라 작성하는 방법이 다르다.

### 참고하기
- 기본적으로 컴파일러는 정수 리터럴을 int 타입 값으로 간주한다.
- 그래서 int 타입의 허용 범위를 초과하는 리터럴은 뒤에 소문자 l이나 대문자 L을 붙여 long 타입 값임을 컴파일러에게 알려줘야 함
```java
long var1 = 10;
long var2 = 20L;
long var3 = 100000000000; //컴파일러는 int로 간주하기 때문에 에러 발생
long var4 = 100000000000L; 
```

## `2.3 문자 타입`
- 하나의 문자를 작은따옴표(')로 감싼 것을 `문자 리터럴`이라고 한다.
- 문자 리터럴은 유니코드로 변환되어 저장된다.
- 유니코드란 세계 각국 문자를 0~65535(2^16-1) 숫자로 매핑한 국제 표준 규약
- 자바는 이러한 유니코드를 저장할 수 있도록 char 타입 제공
  ```java
  char var1 = 'A'; //'A' 문자와 매핑되는 숫자 : 65로 대입
  char var2 = '가'; //'가' 문자와 매핑되는 숫자 : 44032로 대입
  ```
- 유니 코드가 정수이므로 char 타입도 정수 타입에 속한다. 따라서 작은따옴표로 감싼 문자가 아닌 유니코드 숫자를 직접 대입도 가능
  ```java
  char c = 65;      //10진수 65와 매핑되는 문자 : 'A'
  char c = 0x0041;  //16진수 0x0041과 매핑되는 문자 : 'A'
  ```
- 빈 문자열 대입할 경우 컴파일 에러, 초기화 목적이라면 공백(유니코드:32) 포함해서 초기화 해야함
```java
char c ='';   //컴파일 에러
char c =' ';  //공백 하나를 포함해서 초기화
```

## `2.4 실수 타입`

### float, double
|타입|메모리 크기|저장되는 값의 허용 범위(양수 기준)|유효 소수 이하 자리|
|:--:|:--:|:--:|:--:|
|float|4byte|32bit|1.4 * `10^-45` ~ 3.4 * `10^38`|7자리|
|double|8byte|64bit|4.9 * `10^-324` ~ 1.8 * `10^308`|15자리|
- double 타입이 float타입 보다 큰 실수를 저장할 수 있고 정밀도 또한 높다.
- 자바는 IEEE754 표준에 근거하여 float 타입 과 double 타입의 값을 `floation-point`방식 으로 메모리에 저장한다.
- float (32bit)
  - 부호 1bit
  - 지수 8bit
  - 가수 23bit
- double (64bit)
  - 부호 1bit 
  - 지수 11bit
  - 가수 52bit
- 10진수 리터럴
  ```java
  double x = 0.25;
  double y = -3.14;
  ```
- e 또는 E가 포함된 10의 거듭제곱 리터럴
```java
double x = 5e2;     //5.0 * 10^2 = 500.0
double y = 0.12E-2  //0.12 * 10^-2 = 0.0012
```
- 컴파일러는 기본적으로 double타입으로 해석하므로 float타입으로 대입하고 싶으면 f나 F를 붙여 사용
  ```java
  double var1 = 3.14;
  float var2 = 3.14f;
  ```
- double 타입이 float타입 보다 약 2배의 유효 자릿수를 가진다고 보면 됨

## `2.5 논리 타입`
- `참과 거짓을 의미하는 논리 리터럴은 true와 false이다.`
  ```java
  boolean stop = true;
  boolean stop = false;
  ```
- boolean 타입 변수는 주로 두 가지 상태값을 저장할 필요가 있을 경우 사용되며
- 상태값에 따라 조건문과 제어문의 실행 흐름을 변경ㅇ하는데 사용
- 연산식 중에서 비교 및 논리 연산의 산출값은 true or false이므로 boolean 타입 변수에 다음과 같이 대입 가능
  ```java
  int x = 10;
  boolean result = (x==20);
  result = (x != 20);
  result = (x > 20) ;
  result = ( 0 < x && x < 20>);
  ```

## `2.6 문자열 타입`
- String 타입은 자바 기본 타입에 속하지 않는 참조 타입이다.

### 이스케이프 문자
- 문자열 내부에 역슬래쉬(\\)가 붙은 문자를 사용할 수 있다.
- 이것을 이스케이프(escape) 문자라고 한다.
- \\", \\', \\, \\u16진수, \\t(출력 시 탭만큼 띄움), \\n(출력 시 줄바꿈, 라인피드), \\r(출력 시 캐리지 리턴)
  ```java
  String name = "\"ds\"";
  ```
- Java 13부터는 다음과 같은 텍스트 블록 문법을 제공
  ```java
  String str = """
  나는 자바를 \
  학습합니다.
  자바 고수가 될 겁니다.
  """;
  System.out.println(str);
  ```
  > 큰 따옴표 3개로 감싸면 이스케이프하거나 라인피드를 할 필요가 없다. 그리고 \를 사용하면 줄바꿈하지 않고 이어서 작성됨
  - 출력
  ```
  나는 자바를 학습합니다.
  자바 고수가 될 겁니다.
  ```

## `2.7 자동 타입 변환`
- 자동 타입 변환은 값의 허용 범위가 작은 타입이 허용 범위가 큰 타입으로 대입될 때 발생한다.
- 기본 타입의 허용 범위 순
  ```
  byte < short, char < int < long < float < double
  ```
  ```java
  byte byteValue = 10;
  int intValue = byteValue //자동 타입 변환됨
  ```
- 정수 타입이 실수 타입으로 대입될 경우에는 무조건 자동 타입 변환이 된다. 실수 타입은 정수 타입보다 허용 범위가 더 크기 때문
  ```java
  long longValue = 5000000000L;
  float floatValue = longValue;   //5.0E9f로 저장됨
  double doubleValue = longValue; //5.0E9로 저장됨
  ```
- char 타입의 경우 int 타입으로 자동 변환되면 유니코드 값이 int 타입에 대입된다.
  ```java
  char charValue = 'A';
  int intValue = charValue;   //65가 저장됨
  ```
- byte가 char에 대입되는 것은 안된다. 왜냐하면 char 타입의 허용 범위는 음수를 포함하지 않기 때문이다.
  ```java
  byte byteValue = 65;
  char charValue = byteValue; //컴파일 에러
  ```

## `2.8 강제 타입 변환`
- 큰 허용 범위 타입은 작은 허용 범위 타입으로 자동 타입 변환될 수 없다.
- 마치 큰 그릇을 작은 그릇에 담을 수 없는 말과 같다.
- 큰 그릇을 작은 그릇에 담으려면 큰 그릇을 작은 그릇 크기만큼 쪼개서 담아야 한다.
- 이러한 논리로 큰 허용 범위 타입을 작은 허용 범위 타입으로 쪼개어서 저장하는 것을 `casting(캐스팅)`이라고 한다.
- 작은 허용 범위 타입  = (작은 허용 범위 타입)큰 허용 범위 타입 -> `강제 타입 변환`

### int -> byte
```java
int intValue = 10;
byte byteValue = (byte)intValue;
```
- int 타입은 byte 타입보다 큰 허용 범위이기 때문에 (byte) 캐스팅을 하여 타입을 강제 변환 시켜야 한다.
- 이때 byte 는 1byte 크기이고 int 는 4byte이기 때문에 intValue의 앞 3byte가 날라가며 저장된다.
- 따라서 intValue가 1byte로 나타낼 수 없을 경우 원래 값이 보존되지 않는다.
- byte 타입으로 변환할 시 byte의 범위인 (-128 ~ 127) 만 원래 값을 보존할 수 있다.

### long -> int
```java
long longValue = 300;
int intValue = (int)longValue;
```

### int -> char
```java
int intValue = 65;
char charValue = (char) intValue;
System.out.println(charValue);    // 'A'가 출력
```
- int타입은 char타입보다 큰 허용 범위를 가진다.
- char 타입의 허용 범위인 (0~65535) 사이의 값만 원래 값을 유지할 수 있다.

### 실수 -> 정수
```java
double doubleValue =3.14;
int intValue = (int) doubleValue; //정수 부분인 3 만 저장
```
- `실수 타입 (float, double)은 정수 타입(byte, short, int, long)보다 항상 큰 허용 범위를 가진다.`
- 따라서 실수 타입은 정수 타입으로 항상 캐스팅해서 강제 변환시켜야 한다.
- 이때 소수점 이하 부분은 버려지고 정수 부분만 저장된다.


## `2.9 연산식에서 자동 타입 변환`
- 자바는 실행 성능을 향상시키기 위해 컴파일 단계에서 연산을 수행
  ```java
  byte result = 10 + 20     //컴파일: byte result = 30
  ```
  - 자바 컴파일러는 컴파일 단계에서 10 + 20을 미리 연산해서 30으로 만들고 result변수에 30을 저장
  - 따라서 실행 시 덧셈 연산이 없으므로 실행 성능이 좋아진다.
  - 하지만 정수 리터럴이 아니라 변수가 피연산자로 사용되면 실행 시 연산을 수행한다.

### 정수 타입 변수의 산술 연산식
- 정수 타입 변수가 산술 연산식에서 피연산자로 사용되면 int 타입보다 작은 byte, short 타입의 변수는 int타입으로 자동 타입 변환되어 연산을 수행한다.
  ```java
  byte x = 10;
  byte y = 20;
  byte result = x + y; //Compile Error
  int result = x + y;
  ```
  > 이처럼 byte 변수 x,y가 피연산자로 사용되면 변수값은 int 타입으로 변환되어 연산되며 결과도 int타입으로 생성된다. 따라서 특별한 이유가 없다면 int타입으로 변수를 선언하는 것이 타입 변환이 발생하지 않기 때문에 성능이 좋음
- int 타입보다 허용 범위가 더 큰 long 타입이 피연산자로 사용되면 다른 피연산자는 모두 long타입으로 변환되어 연산 되므로 결과 타입도 long이다.
  ```java
  byte v1 = 1;
  int v2 = 2;
  long v3 = 3;
  long result = v1 + v2 + v3;
  int result = v1 + v2 + v3;  //Compile Error
  ```
  > 자바에서는 이항 연산을 실행할 때 같은 타입으로 변환 후 연산한다. 따라서 v1,v2,v3는 long타입으로 자동 타입 변환되어 연산됨

### 실수 타입 변수의 산술 연산식
- 동일한 실수 타입이라면 해당 타입으로 연산된다.
  ```java
  float result = 1.2f + 3.4f; //Compile : float result = 4.6f;
  ```
- 하지만 피연산자 중 하나가 double 타입이면 다른 피연산자도 double타입으로 변환되어 연산되고, 결과 또한 double
  ```java
  double result = 1.2f + 3.4;   //Compile : double result = 4.6;
  ```
- int 타입과 double 타입을 연산하는 경우에도 int 타입 피연산자가 double 타입으로 자동 변환되고 연산이 수행된다.
  ```java
  int intValue = 10;
  double doubleValue = 5.5;
  double result = intValue + doubleValue;   //10.0 + 5.5
  ```
- 만약 int 타입으로 연산을 해야 한다면 캐스팅하면 됨
  ```java
  int intValue = 10;
  double doubleValue = 5.5;
  int result = intValue + (int)doubleValue; //10 + 5
  ```

### 정수 타입 실수 타입 산술 연산식 주의 할 것
```java
int x = 1;
int y = 2;
double resuslt = x / y;
System.out.println(result);   //0.0
```
- 정수 타입 피연산자들의 연산 결과는 항상 정수 이기 때문에 0이 먼저 계산된 후에 double로 바뀌어 0.0이 출력됨
- 해결방법
  1. 둘 다 double로 타입 변환
  ```java
  int x = 1;
  int y = 2;
  double resuslt = (double)x / (double)y;
  System.out.println(result);   //0.5
  ```
  2. x만 double로 타입 변환
  ```java
  int x = 1;
  int y = 2;
  double resuslt = (double)x / y;
  System.out.println(result);   //0.5
  ```
  3. y만 double로 타입 변환
  ```java
  int x = 1;
  int y = 2;
  double resuslt = x / (double)y;
  System.out.println(result);   //0.5
  ```
  > 2,3 의 경우 x,y연산 시에 자동으로 x or y 가 double로 타입 변환되어 연산된다.
- 주의할 Code
  ```java
  int x = 1;
  int y = 2;
  double resuslt = (double)(x /y);
  System.out.println(result);   //0.0
  ```
  > x,y가 int로 연산되어 결과가 0 이 나온 후 double로 변환되기 때문에 결과 값은 0.0

### 문자열과 숫자 더하기
- 자바에서 '+'연산자는 두 가지 기능을 가지고 있다.
  1. 피연산자가 모두 숫자일 경우 덧셈 연산 수행
  2. 피연산자 중 하나가 문자일 경우 나머지 피연산자도 문자열로 자동 변환되어 문자열 결합 연산 수행
```java
int value = 3 + 7;  //int value = 10;
String str1 = "3" + 7 // String str = "37";
String str2 = 3 + "7" // String str = "37";
```
- 연산식에서 '+' 연산자가 연이어 나오면 앞에서부터 순차적으로 덧셈 연산을 수행
- 먼저 수행된 연산이 덧셈이라면 덧셈 결과를 가지고 그 다음 '+'연산을 수행한다
- 만약 먼저 수행된 연산이 문자열 결합 연산이라면 이후 모든 '+'연산은 결합 연산이 된다.
```java
int value = 1 + 2 + 3; //int value = 6;
String str1 = 1 + 2 + "3";  // String str = "33";
String str2 = 1 + "2" + 3;  // String str = "123";
String str3 = "1" + 2 + 3;  // String str = "123";
```
- 앞에서 순차적으로 + 연산을 수행하지 않고 특정 부분을 우선 연산하고 싶으면 해당 부분을 괄호()로 감싸면 된다.
```java
String str = "1" + (2+3); // String str = "15";
```