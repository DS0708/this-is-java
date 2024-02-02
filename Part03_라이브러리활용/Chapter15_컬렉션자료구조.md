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

