# 자바의 정석 - Part03 - Chapter15 컬렉션 자료구조

## 15.1 컬렉션 프레임워크

### 컬렉션 프레임워크란 ?
- 자바는 널리 알려져 있는 `자료구조`를 바탕으로 객체들을 효율적으로 추가, 삭제, 검색할 수 있도록 관련된 인터페이스와 클래스들을 `java.util` 패키지에 포함시켜 놓았다. 
- 이들을 총칭해서 Collection Framework라고 부른다.

### `Collection`
- List
  - `순서를 유지하고 저장`
  - 중복 저장 가능
  - 구현 클래스
    1. ArrayList
    2. Vector
    3. LinkedList
- Set
  - `순서를 유지하지 않고 저장`
  - 중복 저장 불가능
  - 구현 클래스
    1. HashSet
    2. TreeSet
### `Map`
- `키와 값으로 구성된 엔트리 저장`
- 키는 중복 저장 안됨
- 구현 클래스
  1. HashMap
  2. HashTable
  3. TreeMap
  4. Properties

-  List와 Set은 객체를 추가, 삭제, 검색하는 방법에 있어서 공통점이 있기 때문에 공통된 메소드만 따로 모아 `Collection 인터페이스`로 정의해 두고 이것을 상속하고 있다.
-  `Map`은 키와 값을 하나의 쌍으로 묶어서 관리하는 구조로 되어 있어 List 와 Set과는 사용 방법이 다르다.

## 15.2 List 컬렉션

### List란 ?
- List 컬렉션은 객체를 인덱스로 관리하기 때문에 인덱스로 객체를 검색, 삭제할 수 있는 기능 제공
- List Collection에는 ArrayList, Vector, LinkedList등이 있음
- `공통적으로 사용 가능한 List Methods`
  1. 객체 추가
    - boolean add(E e) : 객체 e를 맨 끝에 추가
    - void add(int index, E e) : 객체 e를 index에 추가
    - set(int index, E e) : index자리를 객체 e로 바꿈
  2. 객체 검색
    - boolean contaions(Object o) : 주어진 객체가 저장되어 있는지 여부
    - E get(int index) : 주어진 index에 저장된 객체 return
    - boolean isEmpty() : Collection이 비어 있는지 조사, 비어 있으면 true
    - int size() : 저장되어 있는 전체 객체 수 return
  3. 객체 삭제
    - void clear() : 저장된 모든 객체를 삭제
    - E remove(int index) : 주어진 index에 저장된 객체를 삭제
    - boolean remove(Object o) : 주어진 객체를 삭제

### ArrayList
- 일반적으로 List 컬렉션에서 가장 많이 사용된다.
- 객체를 추가하면 내부 배열에 객체가 저장된다.
- 일반 배열과의 차이점은 ArrayList는 제한 없이 객체 추가 가능
- List 컬렉션은 객체 자체를 저장하는 것이 아니라 객체의 번지, 즉 주소값을 저장한다.
- 동일한 객체를 중복으로 저장할 수 있으며, 이때 동일한 주소값이 저장된다.
- null 값 저장 가능
- ArrayList선언방법
```java
List<E> list = new ArrayList<E>(); //E에 지정된 타입의 객체만 저장
List<E> list = new ArrayList<>(); //E에 지정된 타입의 객체만 저장
List list = new ArrayList();      // 모든 타입의 객체를 저장
```



