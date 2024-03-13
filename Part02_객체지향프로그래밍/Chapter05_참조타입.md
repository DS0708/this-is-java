# 이것이 자바다 - Part05 - Chapter05 참조 타입

## 목차
- [5.1 데이터 타입 분류](#51-데이터-타입-분류)
- [5.2 메모리 사용 영역](#52-메모리-사용-영역)
- [5.3 참조 타입 변수의 ==, != 연산](#53-참조-타입-변수의---연산)

## `5.1 데이터 타입 분류`
자바의 데이터 타입은 크게 `기본 타입(primitive type)과 참조 타입(reference type)`으로 분류된다.

### 데이터 타입
- 기본 타입
  - 정수 타입 : byte, char, short, int, long
  - 실수 타입 : float, double
  - 논리 타입 : boolean
- 참조 타입
  - 배열 타입
  - 열거 타입
  - 클래스
  - 인터페이스
> 기본 타입으로 선언된 변수와 참조 타입으로 선언된 변수의 차이점은 저장되는 값이다.
> 기본 타입으로 선언된 변수는 값 자체를 저장하지만 참조 타입으로 선언된 변수는 객체가 생성된 메모리 번지를 저장한다.

### 예시
```java
// 기본 타입 변수
int age = 25;
double price = 100.5;

// 참조 타입 변수
String name = "신용권";
String hobby = "독서";
```

<img src="./image/reType.png" width="600" height="400"/>

- 변수들은 모두 Stack이라는 메모리 영역에 생성된다.
- 기본 타입 변수인 age와 price는 직접 값을 저장하고 있다.
- 참조 타입 변수인 name과 hobby는 힙 메모리 영역의 String 객체 번지를 저장하고 이 번지를 통해 String 객체를 참조한다.


## `5.2 메모리 사용 영역`
java 명령어로 JVM이 구동되면 JVM은 OS에서 할당받은 `메모리 영역(Runtime Data Area)`을 다음과 같이 구분해서 사용한다.

<img src="./image/RuntimeDataArea.png" width="400" height="600"/>

### 메소드 영역
- 바이트코드 파일을 읽어 내용이 저장되는 영역
- 클래스별로 상수, 정적 필드, 메소드 코드, 생성자 코드 등이 저장된다.

### 힙 영역
- 객체가 생성되는 영역
- 객체의 번지는 메소드 영역과 스택 영역의 상수와 변수에서 참조할 수 있다.

### 스택 영역
- 메소드를 호출할 때마다 생성되는 Frame이 저장되는 영역
- 메소드 호출이 끝나면 Frame은 자동 제거
- Frame 내부에는 로컬 변수 스택이 존재하며, 여기에서 기본 타입 변수와 참조 타입 변수가 생성되고 제거된다.


## `5.3 참조 타입 변수의 ==, != 연산`
- `==, != 연산자는 변수의 값이 같은지, 아닌지를 조사한다.`
- 참조 타입 변수의 값은 객체의 번지이므로
참조 타입 변수의 ==, != 연산자는 `번지수가 같은지 비교하는 것`이 된다.

<img src="./image/reEqual.jpeg" width="400" height="300"/>

```
refVar1 == refVar2  -> false
refVar2 == refVar3  -> true
```

- 물론 같은 값들을 가지더라도 번지수가 다르면 다르다.

```java
int [] arr1 = new int[]{1,2,3};
int [] arr2 = new int[]{1,2,3};
int [] arr3 = arr2;

System.out.println(arr1 == arr2);
System.out.println(arr2 == arr3);
```
```
결과
 
false
true
```



