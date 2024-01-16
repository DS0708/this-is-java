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

