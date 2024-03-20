---
tags: java, collections, Set, HashSet, TreeSet, LinkedHashSet, Iterator
---
## 중복 없는 데이터의 집합을 다룰 때 Set을 사용

Java에서는 중복 없는 데이터의 집합을 다룰 때 `Set` 인터페이스와 그 구현체들을 사용합니다. 아래는 `HashSet`, `LinkedHashSet`, `TreeSet` 클래스의 사용 예시와 주요 메서드에 대한 설명입니다.

treeser : 하나의 형만 저장 가능
hashset : 다흔 형 저장 가능
## 코드 예제

```java
import java.util.HashSet;
import java.util.LinkedHashSet;
import java.util.TreeSet;
import java.util.Set;
```
### 선언
```java
HashSet<형> hashset = new HashSet<>();
HashSet<형> set5 = new HashSet<형>(10, 0.7f);
TreeSet<형> treeset = new TreeSet<>();
// 초기 capacity와 load factor를 지정
// 기본 생성 시 initial capacity는 16, load factor는 0.75
// 데이터 초과 입력 시 저장 용량은 2배로 증가. 과부하 발생 가능
// 초기 데이터 개수를 알고 있다면, 초기 용량 지정이 좋습니다.
```
### 값 추가/제거
```java
boolean add(E e)
//- 값 없어서 추가시 true / 중복시 false 반환
set.remove("a");
//- 요소 삭제 - 값 존재시 삭제후 true / 없을시 false 반환 set.clear();//모든 값 제거
```
### 값 출력
```java
////           TreeSet 출력                  ////
System.out.println(set); //전체출력 [2,3,4]
System.out.println(set.first());//최소값 출력
System.out.println(set.last());//최대값 출력
System.out.println(set.higher(3));
//입력값보다 큰 데이터중 최소값 출력 없으면 null
System.out.println(set.lower(3));
//입력값보다 작은 데이터중 최대값 출력 없으면 null

Iterator<E> iter = set.iterator();	// Iterator 사용

//값이 있으면 true 없으면 false
while(iter.hasNext()) {
    System.out.println(iter.next());
}

for(String value : set) {
     System.out.print("("+value+")"); // 반복 출력
}

import java.util.Iterator;
// Iterator 사용해 hashSet 데이터 출력 실시
Iterator iterator = hashSet.iterator();
while(iterator.hasNext()){
    int data = (int) iterator.next(); //int 형변환
    System.out.println("HashSet Data : " + data);	
}java ```
```
```

### Set 클래스 주요 메서드
``` java
boolean add(E e); // 요소를 추가합니다.
int size(); // 집합의 크기를 반환합니다.
boolean contains(Object o); // 집합이 특정 요소를 포함하고 있는지 확인합니다 (true/false).
set.containsAll(set2); // 하나의 집합이 다른 집합의 모든 요소를 포함하고 있는지 확인합니다 (true/false).
set.addAll(set2); // 하나의 집합에 다른 집합의 모든 요소를 추가합니다 (중복된 요소는 제거됩니다).
set.isEmpty(); // 집합이 비어 있는지 확인합니다.
boolean remove(Object o); // 특정 요소를 집합에서 제거합니다.
retainAll(); // 두 집합의 교집합을 반환합니다.
removeAll(); // 두 집합의 차집합을 반환합니다.
```
- **HashSet**
    - *해시를 이용한 Set의 구현 클래스*
    - *요소의 추가나 검색이 빠르지만, 순서가 없으므로 순서와 무관하게 저장된다*
    - *검색 후 추가 삭제 해야한다*
    - *List구조에 비해 느립니다*

- **LinkedHashSet**
    - *HashSet에서 순서를 부여한 클래스*

- **TreeSet**
    - *트리 구조를 이용한 Set의 구현 클래스*
    - *자연적으로 요소가 순서화되어있음*
    - *Comparator를 설정함으로써 임의의 순서로도 데이터를 보관 및 유지할 수 있다*

