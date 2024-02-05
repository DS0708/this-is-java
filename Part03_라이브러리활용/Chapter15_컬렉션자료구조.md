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

### `ArrayList`
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
- 특정 인덱스의 객체를 제거하면 바로 뒤 인덱스부터 마지막 인덱스까지 모두 앞으로 1씩 당겨지므로 `삭제와 삽입이 빈번히 일어나는 곳에 사용 하는 것은 바람직하지 않다.`
- for문 활용 예시
```java
List<Integer> list = new ArrayList<>();
for (int i : list) System.out.println(i);
```

### `Vector`
- ArrayList와 동일한 내부 구조
- 차이점은 Vector은 Synchronized 메소드로 구성되어 있기 때문에 `멀티 스레드가 동시에 Vector() 메소드를 실행할 수 없음.`
- 따라서 `멀티 스레드 환경에서는 안전하게 객체를 추가 또는 삭제할 수 있음`
- 선언방법
```java
List<E> list = new Vector<E>();  //E에 지정된 타입의 객체만 저장
List<E> list = new Vector<>();  //E에 지정된 타입의 객체만 저장
List list = new Vector(); //모든 타입의 객체 저장
```
- 멀티 스레드 환경 사용 예시
```java
List<Integer> list = new Vector<>();

Thread th1 = new Thread() {
  @Override
  public void run(){
    for (int i=0; i<1000; i++) list.add(i);
  }
};

Thread th2 = new Thread() {
  @Override
  public void run(){
    for (int i=0; i<1000; i++) list.add(i);
  }
};

th1.start();
th2.start();

try {
  th1.join();
  th2.join();
} catch (Exception e) {}

System.out.println(list.size()); //2000
```
> 실행 결과가 정확히 200임, ArrayList를 사용할 경우 2000이 나오지 않는다.

### `LinkedList`
- ArrayList와 사용방법은 동일하나 내부 구조가 완전히 다름
- LinkedList는 인접 객체를 체인처럼 연결해서 관리
- 특정 위치에서 객체를 삽입하거나 삭제하면 바로 앞뒤 링크만 변경하면 되므로 `빈번한 객체 삭제와 삽입이 일어나는 곳에 유리`
- 생성방법
```java
List<E> list = new LinkedList<E>(); //E에 지정된 타입의 객체만 저장
List<E> list = new LinkedList<>(); //E에 지정된 타입의 객체만 저장
List list = new LinkedList();      // 모든 타입의 객체를 저장
```

## 15.3 Set 컬렉션
- List 컬렉션은 저장 순서를 유지하지만, `Set 컬렉션은 저장 순서가 유지되지 않는다.`
- 객체 중복 저장 불가능, 하나의 null만 저장 가능
- 수학의 집합과 같은 구조
- HashSet, LinkedHashSet, TreeSet 등이 존재
- Set 인터페이스의 메소드
  - 객체 추가
    - boolean add(E e) : 저장을 성공하면 true, 실패하면 false를 return
  - 객체 검색
    - boolean contains(Object o) : 객체가 저장되어 있는지 여부
    - isEmpty()
    - `Iterator<E> iterator() : 저장된 객체를 한 번씩 가져오는 반복자 리턴`
    - int size() : 저장되어 있는 전체 객체 수 리턴
  - 객체 삭제
    - void clear() : 저장된 모든 객체 삭제
    - boolean remove(Object o) : 주어진 객체 삭제

### `HashSet`
- Set 컬렉션 중 가장 많이 사용됨
- 생성 방법
```java
Set<E> set = new HashSet<E>();
Set<E> set = new HashSet<>();
Set set = new HashSet();  //모든 타입의 객체를 저장
```
- HashSet은 동일한 객체는 중복 저장하지 않는다.
  - 여기서 동일한 객체란 동등 객체를 의미
  - 다른 객체이더라도 hashCode() 메소드의 리턴값이 같고
  - equals() 메소드가 true를 리턴하면 동일한 객체라고 판단하고 중복저장하지 않는다.
- Code Example
  1. `HashSet사용`
  ```java
  Set<String> set = new HashSet<>();

  set.add("JAVA");
  set.add("JDBC");
  set.add("JAVA"); //중복 객체

  System.out.println(set.size()); // 2
  ```
  2. `class에 hashCode() 와 equals()를 Override하여 사용하기`
  ```java
  import java.util.HashSet;
  import java.util.Set;

  public class set {
      public static void main(String[] args) {
          Set<Member> set = new HashSet<>();

          set.add(new Member("ds",25));
          set.add(new Member("ds",25));

          System.out.println("총 객체 수 : " + set.size()); // 총 객체수 : 1
      }
  }

  class Member{
      String name;
      int age;

      public Member(String name, int age){
          this.name = name;
          this.age = age;
      }

      //hashCode 재정의
      @Override
      public int hashCode(){
          return name.hashCode() + age;
      }
      
      //equals 재정의
      @Override
      public boolean equals(Object obj){
          if(obj instanceof Member target){
              return target.name.equals(this.name) && (target.age==this.age);
          }else{
              return false;
          }
      }
  }
  ```
  > hashCode 값이 같고 equals가 true를 리턴하면 동일한 객체로 판별한다.(둘 중 하나라도 틀리면 다른 객체임)
  3. `Set에 있는 객체 불러오기`
  ```java
  //for 문 사용하기
  Set<E> set = new HashSet<>();
  for(E e : set){
    ...
  }
  ```
  ```java
  //ierator 사용하기
  Set<E> set = new HashSet<>();
  Iterator<E> iterator = set.iterator();

  while(iterator.hasNext()){
    E e = iterator.next();
  }
  ```
  > hasNext()로 가져올 객체가 있는지 확인하고 next()를 통해 객체를 가져온다.

## 15.4 Map 컬렉션
- Key와 Value로 구성된 Entry 객체를 저장한다.
- 여기서 Key와 Value 모두 Object임
- Key는 중복저장 불가능, Value는 가능
- 기존에 저장된 Key와 동일한 Key로 값을 저장할 경우 새로운 Key의 Value로 대체된다.
- HashMap, Hashtable, LinkedHashMap, Properties, TreeMap 등이 있다.
- Map 인터페이스 Method (키로 객체들을 관리하기 때문에 키를 매개값으로 갖는 메소드가 많다.)
  - 객체 추가
    - V put(K key, V value) : 주어진 key와 value를 추가하고 value를 리턴
  - 객체 검색
    - boolean containsKey(Object key) : 주어진 key가 있는지 여부
    - boolean containsValue(Object value) : 주어진 value가 있는지 여부
    - Set<Map.Entry<K,V>> entrySet() : 키와 값의 쌍으로 구성된 모든 Map.Entry 객체를 Set에 담아서 리턴
    - V get(Object key) : 주어진 key의 value를 리턴
    - boolean isEmpty()
    - Set<K> keySet() : 모든 key를 Set에 담아서 리턴
    - int size() : 저장된 키의 총 수를 리턴
    - Collection<V> values() : 저장된 모든 value를 Collection에 담아서 리턴
  - 객체 삭제
    - void clear() : 모든 Map.Entry(키와 값)을 삭제
    - V remove(Object key) : 주어진 key와 일치하는 Map.Entry를 삭제하고 그 value를 리턴


### `HashMap`
- HashMap은 키로 사용할 객체가 hashCode() 메소드의 리턴값이 같고 equals() 메소드가 true를 리턴할 경우, 동일 키로 보고 중복 저장을 허용하지 않음.
- 생성 방법
```java
Map<K,V> map = new HashMap<K,V>();
```
```java
Map<String,Integer> map = new HashMap<String,Integer>();
Map<String,Integer> map = new HashMap<>();
Map map = new HashMap();  //거의 없음
```
- Code Example
```java
import java.util.HashMap;
import java.util.Iterator;
import java.util.Map;
import java.util.Set;

public class HashMapExample {
    public static void main(String[] args) {
        Map<String, Integer> map = new HashMap<>();

        map.put("ds",90);
        map.put("sh",95);
        map.put("ds",100);  //동일한 key

        System.out.println(map.size());     //2

        //키로 값 얻기
        String key = "ds";
        int value = map.get(key);
        System.out.println(value);  //100

        //키 Set 컬렉션을 얻고, 반복해서 키와 값을 얻기
        Set<String> keySet = map.keySet();
        Iterator<String> keyIterator = keySet.iterator();
        while(keyIterator.hasNext()){
            String k = keyIterator.next();
            Integer v = map.get(k);
            System.out.println("set Collection : "+k+" : "+v);
        }

        //엔트리 Set 컬렉션을 얻고, 반복해서 키와 값을 얻기
        Set<Map.Entry<String,Integer>> entrySet = map.entrySet();
        Iterator<Map.Entry<String,Integer>> entryIterator = entrySet.iterator();
        while(entryIterator.hasNext()){
            Map.Entry<String,Integer> entry = entryIterator.next();
            String k = entry.getKey();
            int v = entry.getValue();
            System.out.println("엔트리 set :" + k+" : "+v);
        }

        //키로 엔트리 삭제
        map.remove("sh");
        System.out.println(map.size()); // 1
    }
}
```

### `Hashtable`
- HashMap과 동일한 내부 구조
- 차이점은 Hashtable은 `synchronized 메소드로 구성`
- 따라서 멀티 스레드 환경에서 안전하게 객체를 추가 삭제할 수 있음.
- 선언방법
```java
Map<String,Integer> map = new Hashtable<String,Integer>();
Map<String,Integer> map = new Hashtable<>();
```

### `Properties`
- Properties는 `Hashtable의 자식 클래스`이기 때문에 Hashtable의 특징을 그대로 가지고 있다.
- Properties는 Key와 Value를 `String 타입으로만 제한한 컬렉션`
- 주로 확장자가 .properties인 프로퍼티 파일을 읽을 때 사용
- Code Example
  - database.properties
  ```properties
  driver=oracle.jdbc.OracleDirver
  url=jdbc:oracle:thin:@localhost:1521:orcl
  username=scott
  password=tiger
  admin=\uD64D\uAe38\uB3D9
  ```
  - PropertiesExample
  ```java
  import java.io.IOException;
  import java.util.Properties;

  public class PropertiesExample {
      public static void main(String[] args) throws IOException {
          Properties properties = new Properties();

          //PropertiesExample.class와 동일한 ClassPath에 있는 database.properties 파일 로드
          properties.load(PropertiesExample.class.getResourceAsStream("database.properties"));

          //주어진 키에 대한 값 읽기
          String driver = properties.getProperty("driver");
          String url = properties.getProperty("url");
          String username = properties.getProperty("username");
          String password = properties.getProperty("password");
          String admin = properties.getProperty("admin");

          //값 출력
          System.out.println("driver : "+ driver);
          System.out.println("url : "+ url);
          System.out.println("username : "+ username);
          System.out.println("password : "+ password);
          System.out.println("admin : "+ admin);
      }
  }
  ```
 
## 15.5 검색 기능을 강화시킨 컬렉션 `(TreeSet, TreeMap)` 
- 컬렉션 프레임 워크는 검색 기능을 강화시킨 TreeSet과 TreeMap 제공
- TreeSet은 Set 컬렉션이고 TreeMap은 Map컬렉션이다.

### TreeSet
- Binary tree (이진 트리)를 기반으로 한 Set Collection
- 이진 트리는 여러개의 노드가 트리형태로 연결된 구조로, 루트 노드라고 불리는 하나의 노드에서 시작해 각 노드에 최대 2개의 노드를 연결할 수 있는 구조
- TreeSet에 객체를 저장하면 부모노드의 객체와 비교해 낮은 것은 왼쪽, 높은 것은 오른쪽 자식 노드에 자동으로 배치
- 생성 방법
  ```java
  TreeSet<E> treeSet = new TreeSet<E>();
  TreeSet<E> treeSeet = new TreeSeet<>();
  ```
  > Set 타입 변수에 대입해도 되지만 TreeSet 타입으로 대입한 이유는 검색 관련 메소드가 TreeSet에만 정의되어 있기 때문이다.
- 관련 메소드
  - E first() : 제일 낮은 객체 리턴
  - E last() : 제일 높은 객체 리턴
  - E lower(E e) : 주어진 객체보다 바로 아래 객체 리턴
  - E higher(E e) : 주어진 객체보다 바로 위 객체 리턴
  - E floor(E e) : 주어진 객체와 동등한 객체가 있다면 리턴, 없다면 바로 아래 객체 리턴
  - E ceiling(E e) : 주어진 객체와 동등한 객체가 있다면 리턴, 없다면 바로 위 객체 리턴
  - E pollFirst() : 제일 낮은 객체를 리턴하고 컬렉션에서 제거
  - E pollLast() : 제일 높은 객체를 리턴하고 컬렉션에서 제거
  - Iterator<E> descendingIterator() : 내림차순으로 정렬된 Iterator를 리턴
  - NavigableSet<E> descendingSet() : 내림차순으로 정렬된 NavigableSet을 리턴
  - NavigableSet<E> headSet(E e, boolean i) : e보다 낮은 객체를 리턴, i가 true이면 e를 포함하여 리턴
  - NavigableSet<E> tailSet(E e, boolean i) : e보다 높은 객체를 리턴, i가 true이면 e를 포함하여 리턴
  - NavigableSet<E> subSet(E a, boolean i1, E b, boolean i2) : a보다 크고 b보다 작은 NavigableSet리턴, i1와 i2에 따라 포함 여부 결정
- Code Example
  ```java
  import java.util.Iterator;
  import java.util.NavigableSet;
  import java.util.TreeSet;

  public class TreeSetExample {
      public static void main(String[] args) {
          TreeSet<Integer> treeSet = new TreeSet<>();

          treeSet.add(3);
          treeSet.add(9);
          treeSet.add(1);
          treeSet.add(5);
          treeSet.add(7);

          // 정렬된 Integer 하나씩 꺼내오기
          for (int i : treeSet) System.out.print(i+" ");
          System.out.println();

          // 특정 Integer 객체 가져오기
          System.out.println("가장 낮은 수 : "+ treeSet.first());
          System.out.println("가장 높은 수 : "+ treeSet.last());
          System.out.println("6 아래 수 : "+ treeSet.lower(6));
          System.out.println("6 위의 수 : "+ treeSet.higher(6));
          System.out.println("5이거나 그 아래 수 : "+ treeSet.floor(5));
          System.out.println("6이거나 그 위의 수 : "+ treeSet.ceiling(6));

          //내림차순으로 정렬하기
          NavigableSet<Integer> decendingSet = treeSet.descendingSet();
          for (int i : decendingSet) System.out.print(i+" ");
          System.out.println();

          //범위 검색 (5>=)
          NavigableSet<Integer> rangeSet = treeSet.tailSet(5,true);
          for (int i : rangeSet) System.out.print(i+" ");
          System.out.println();

          //범위 검색 (3< , <=7)
          rangeSet = treeSet.subSet(3,false,7,true);
          for (int i : rangeSet) System.out.print(i+" ");
          System.out.println();
      }
  }
  ``` 

### TreeMap
- 이진 트리를 기반으로 한 Map Collection
- TreeSet과의 차이점은 키와 값이 저장된 `Entry를 저장`
- 키를 기준으로 정렬
- 생성 방법
  ```java
  TreeMap<K,V> treeMap = new TreeMap<K,V>();
  TreeMap<K,V> treeMap = new TreeMap<>();
  ```
- 메소드
  - Map.Entry<K,V> firstEntry() : 제일낮은 Entry 리턴
  - Map.Entry<K,V> lastEntry() : 제일높은 Entry 리턴
  - Map.Entry<K,V> lowerEntry(K key) : key보다 바로 아래 Entry 리턴
  - Map.Entry<K,V> higherEntry(K key) : key보다 바로 위 Entry 리턴
  - Map.Entry<K,V> floorEntry(K key) : key와 동등한 Entry 리턴, 없다면 바로 아래 리턴
  - Map.Entry<K,V> ceilingEntry(K key) : key와 동등한 Entry 리턴, 없다면 바로 위 리턴
  - Map.Entry<K,V> pollFirstEntry() : 제일 낮은 Entry 리턴하고 삭제
  - Map.Entry<K,V> pollLastEntry() : 제일 높은 Entry 리턴하고 삭제
  - NavigableSet<K> descendingKeySet() : 내림차순으로 정렬된 키의 NavigableSet 리턴
  - NavigableMap<K,V> descendingMap() : 내림차순으로 정렬된 NavigableMap 리턴
  - NavigableMap<K,V> headMap(K key,boolean i) : key보다 낮은 Entry들 리턴, i가 true면 key포함
  - NavigableMap<K,V> tailMap(K key,boolean i) : key보다 높은 Entry들 리턴, i가 true면 key포함
  - NavigableMap<K,V> subMap(K k1,boolean i1, K2, boolean i2) : k1보다 높고 k2보다 낮은 Entry리턴, i1와 i2에 따라 k1,k2 포함 여부 결정
- Code Example
  ```java
  import java.util.*;

  public class TreeMapExample {
      public static void main(String[] args) {
          TreeMap<String,Integer> treeMap = new TreeMap<>();

          treeMap.put("apple",10);
          treeMap.put("cherry",20);
          treeMap.put("banana",30);

          //정렬된 엔트리 가져오기
          Set<Map.Entry<String,Integer>> entrySet = treeMap.entrySet();
          for (Map.Entry<String,Integer> entry : entrySet) System.out.println(entry.getKey() + " : " + entry.getValue());
          System.out.println();

          //특정 키에 대한 값 가져오기
          Map.Entry<String,Integer> entry = null;
          entry = treeMap.firstEntry();
          System.out.println("제일 앞 단어 : "+ entry.getKey());
          entry = treeMap.lastEntry();
          System.out.println("제일 뒤 단어 : "+ entry.getKey());
          entry = treeMap.floorEntry("car");
          System.out.println("car와 같은 혹은 앞 단어 : " + entry.getKey());
          System.out.println();

          //내림차순으로 정렬하기
          NavigableMap<String,Integer> descendingMap = treeMap.descendingMap();
          Set<Map.Entry<String,Integer>> descendingEntrySet = descendingMap.entrySet();
          for (Map.Entry<String,Integer> e : descendingEntrySet) System.out.println(e.getKey() + " : " + e.getValue());
          System.out.println();

          //범위 검색
          System.out.println("[b~d 사이의 단어 검색]");
          NavigableMap<String,Integer> rangeMap = treeMap.subMap("b",true,"d",false);
          for (Map.Entry<String,Integer> e : rangeMap.entrySet()) System.out.println(e.getKey() + " : " + e.getValue());
          System.out.println();


      }
  }
  ```

### `Comparable과 Comparator`
- TreeSet와 TreeMap에 저장되는 키는 Comparable인터페이스를 구현해야 저장과 동시에 오름차순으로 정렬될 수 있다.
- Integer, Double, String 타입의 객체는 모두 Comparable이 구현되어 있다.
- 그 외의 객체에는 Comparable 인터페이스를 구현해주어야 TreeSet과 TreeMap이 사용 가능

### Comparable
- Comparable 인터페이스에는 compareTo() 메소드가 정의 되어 있다.
- 따라서 사용자 정의 클래스에서 이 메소드를 Override하여 비교 결과를 정수 값으로 리턴해야 한다.
  - int compareTo(T o)
  - 주어진 객체와 같으면 0 리턴
  - 주어진 객체보다 적응면 음수를 리턴
  - 주어진 객체보다 적응면 양수를 리턴
- Code Example
  ```java
  import java.util.TreeSet;

  public class ComparableExample {
      public static void main(String[] args) {
          TreeSet<Person> treeSet = new TreeSet<>();

          treeSet.add(new Person("ds",25));
          treeSet.add(new Person("sh",26));
          treeSet.add(new Person("dm",23));

          for (Person p : treeSet) System.out.println(p.name+" : "+p.age);
      }
  }

  class Person implements Comparable<Person>{
      String name;
      int age;
      public Person(String name, int age){
          this.name = name;
          this.age = age;
      }
      @Override
      public int compareTo(Person o){
          if(age < o.age) return -1;
          else if (age == o.age) return 0;
          else return 1;
      }
  }
  ```

### Comparator
- 비교 기능이 없는 Comparable 비구현 객체를 저장하고 싶을 때 사용
- TreeSet과 TreeMap을 생성할 때 Comparator를 다음과 같이 제공하면된다.
  ```java
  TreeSet<E> treeSet = new TreeSet<E>( new ComparatorImpl() );
  TreeMap<K,V> treeMap = new TreeMap<K,V>( new ComparatorImpl() );
  ```
- Comparator 인터페이스를 구현한 비교자 객체를 선언하면 됨
- compare() 메소드를 Override해야한다.
  - int compare(T o1, T o2)
  - If o1 = o2, return 0
  - If o1 < o2, return 음수
  - If o1 > o2, return 양수
- Code Example : comparable를 구현하지 않은 Fruit객체를 TreeSet에 저장하는 예
  ```java
  import java.util.Comparator;
  import java.util.TreeSet;

  public class ComparatorExample {
      public static void main(String[] args) {
          TreeSet<Fruit> treeSet = new TreeSet<>(new FruitComparator());

          treeSet.add(new Fruit("포도",3000));
          treeSet.add(new Fruit("수박",10000));
          treeSet.add(new Fruit("딸기",6000));

          for (Fruit fruit : treeSet) System.out.println(fruit.name+" : "+fruit.price);
      }
  }

  class Fruit{
      String name;
      int price;
      public Fruit(String name, int price){
          this.name = name;
          this.price = price;
      }
  }

  class FruitComparator implements Comparator<Fruit>{
      @Override
      public int compare(Fruit o1, Fruit o2){
          if(o1.price < o2.price) return -1;
          else if (o1.price==o2.price) return 0;
          else return 1;
      }
  }
  ```


## 15.6 LIFO 와 FIFO 컬렉션 `(Stack, Queue)`
- LIFO : Last In First Out
- FIFO : First In First Out
- 컬렉션 프레임워크는 LIFO 자료구조를 제공하는 `Stack 클래스`와
- FIFO 자료구조를 제공하는 `Queue의 인터페이스`를 제공한다.

### `Stack` Class
- LIFO
- 선언방법
  ```java
  Stack<E> stack = new Stack<E>();
  Stack<E> stack = new Stack<>();
  ```
- Method
  - E push(E item) : item을 스택에 push
  - E pop() : 스택의 맨 위의 객체를 빼낸다.
- Code Example
  ```java 
  import java.util.Stack;

  public class StackExample {
      public static void main(String[] args) {
          Stack<Integer> stack = new Stack<>();

          stack.push(1);
          stack.push(2);
          stack.push(3);

          while(!stack.isEmpty()){
              System.out.println(stack.pop());
          }
      }
  }
  ```
  ```
  실행결과 :
  3
  2
  1
  ```

### `Queue` Interface
- FIFO
- 선언방법
  ```java
  Queue<E> queue = new LinkedList<E>();
  Queue<E> queue = new LinkedList<>();
  ```
  > Queue 인터페이스를 구현한 대표적인 클래스는 LinkedList이다. 그래서 LinkedList객체를  Queue 인터페이스 변수에 대입.
- Method
  - boolean offer(E e) : 주어진 객체를 큐에 삽입
  - E poll() : 큐에서 객체를 빼낸다.
- Code Example
  ```java
  import java.util.LinkedList;
  import java.util.Queue;

  public class QueueExample {
      public static void main(String[] args) {
          Queue<Integer> queue = new LinkedList<>();

          queue.offer(1);
          queue.offer(2);
          queue.offer(3);

          while(!queue.isEmpty()){
              System.out.println(queue.poll());
          }

      }
  }
  ```
  ```
  실행결과 :
  1
  2
  3
  ```