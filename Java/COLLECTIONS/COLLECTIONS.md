---
tags:
  - java
  - collections
  - SequencedCollection
---
![[Pasted image 20250131150909.png]]

자바 21 SequencedCollection
![[Pasted image 20250131150957.png]]
- SequencedCollection
```java
interface SequencedCollection<E> extends Collection<E> {
    // new method
    SequencedCollection<E> reversed();
    // methods promoted from Deque
    void addFirst(E);
    void addLast(E);

    E getFirst();
    E getLast();

    E removeFirst();
    E removeLast();
}
```
- SequencedSet
```java
interface SequencedSet<E> extends Set<E>, SequencedCollection<E> {

    // covariant override
    SequencedSet<E> reversed();
}
```
- SequencedMap
```java
interface SequencedMap<K, V> extends Map<K, V> {
    // new methods
    SequencedMap<K, V> reversed();
    SequencedSet<K> sequencedKeySet();
    SequencedCollection<V> sequencedValues();
    SequencedSet<Entry<K, V>> sequencedEntrySet();

    V putFirst(K, V);
    V putLast(K, V);

    // methods promoted from NavigableMap
    Entry<K, V> firstEntry();
    Entry<K, V> lastEntry();
    Entry<K, V> pollFirstEntry();
    Entry<K, V> pollLastEntry();
}

```

### **Java JDK 21에서 추가된 `SequencedCollection` 인터페이스**

Java 21에서는 새로운 인터페이스 **`SequencedCollection`**, `SequencedSet`, `SequencedMap`이 추가되었습니다.  
이는 기존 컬렉션 인터페이스인 `List`, `Set`, `Map`에 **앞쪽(`first`), 뒤쪽(`last`) 요소를 쉽게 접근**할 수 있도록 확장한 인터페이스입니다.

---

## **1. `SequencedCollection<E>` 인터페이스**

- 순서를 유지하는 컬렉션에서 **첫 번째(`first()`), 마지막(`last()`) 요소를 쉽게 접근**할 수 있도록 지원.
- 기존 `List`와 `Deque`의 기능을 포함하지만, 더 **일관된 API**를 제공.
- `reversed()` 메서드를 통해 컬렉션을 뒤집을 수 있음.

### **추가된 주요 메서드**

|메서드|설명|
|---|---|
|`E getFirst()`|첫 번째 요소 반환|
|`E getLast()`|마지막 요소 반환|
|`SequencedCollection<E> reversed()`|컬렉션을 반대로 정렬하여 새로운 컬렉션 반환|
|`void addFirst(E e)`|첫 번째 위치에 요소 추가|
|`void addLast(E e)`|마지막 위치에 요소 추가|
|`E removeFirst()`|첫 번째 요소 제거 후 반환|
|`E removeLast()`|마지막 요소 제거 후 반환|

---

## **2. `SequencedSet<E>` 인터페이스**

- `Set`의 특성을 유지하면서, `SequencedCollection` 기능을 추가.
- 순서가 보장되며, `first()` 및 `last()` 메서드 사용 가능.

### **예제: `LinkedHashSet`을 활용한 `SequencedSet`**

```java
import java.util.*;

public class SequencedSetExample {
    public static void main(String[] args) {
        SequencedSet<String> set = new LinkedHashSet<>();
        set.add("A");
        set.add("B");
        set.add("C");

        System.out.println(set.getFirst()); // A
        System.out.println(set.getLast());  // C

        set.addFirst("X");
        System.out.println(set); // [X, A, B, C]

        set.addLast("Z");
        System.out.println(set); // [X, A, B, C, Z]

        set.removeFirst();
        set.removeLast();
        System.out.println(set); // [A, B, C]
    }
}
```

---

## **3. `SequencedMap<K, V>` 인터페이스**

- `Map` 인터페이스를 확장하여 **첫 번째(`firstEntry()`), 마지막(`lastEntry()`) 요소를 쉽게 접근** 가능.
- 순서가 있는 `LinkedHashMap`에서 유용하게 활용 가능.

### **추가된 주요 메서드**

|메서드|설명|
|---|---|
|`Map.Entry<K, V> firstEntry()`|첫 번째 항목 반환|
|`Map.Entry<K, V> lastEntry()`|마지막 항목 반환|
|`SequencedMap<K, V> reversed()`|Map을 반대로 정렬하여 새로운 Map 반환|
|`void putFirst(K key, V value)`|첫 번째 위치에 key-value 추가|
|`void putLast(K key, V value)`|마지막 위치에 key-value 추가|
|`Map.Entry<K, V> pollFirstEntry()`|첫 번째 항목 제거 후 반환|
|`Map.Entry<K, V> pollLastEntry()`|마지막 항목 제거 후 반환|

### **예제: `LinkedHashMap`을 활용한 `SequencedMap`**

```java
import java.util.*;

public class SequencedMapExample {
    public static void main(String[] args) {
        SequencedMap<Integer, String> map = new LinkedHashMap<>();
        map.put(1, "One");
        map.put(2, "Two");
        map.put(3, "Three");

        System.out.println(map.firstEntry()); // 1=One
        System.out.println(map.lastEntry());  // 3=Three

        map.putFirst(0, "Zero");
        System.out.println(map); // {0=Zero, 1=One, 2=Two, 3=Three}

        map.putLast(4, "Four");
        System.out.println(map); // {0=Zero, 1=One, 2=Two, 3=Three, 4=Four}

        map.pollFirstEntry();
        map.pollLastEntry();
        System.out.println(map); // {1=One, 2=Two, 3=Three}
    }
}
```

---

## **4. `List`, `Deque`, `LinkedHashSet`, `LinkedHashMap`의 변화**

- **기존 컬렉션(`ArrayList`, `LinkedList`, `LinkedHashSet`, `LinkedHashMap`)이 자동으로 `SequencedCollection`, `SequencedSet`, `SequencedMap`을 구현하도록 변경됨.**
- 즉, `LinkedList`와 같은 기존 클래스에서도 새로운 메서드를 바로 사용할 수 있음.

```java
import java.util.*;

public class ListExample {
    public static void main(String[] args) {
        List<String> list = new ArrayList<>(List.of("A", "B", "C"));
        
        System.out.println(list.getFirst()); // A
        System.out.println(list.getLast());  // C

        list.addFirst("X");
        list.addLast("Z");
        System.out.println(list); // [X, A, B, C, Z]
    }
}
```

---

## **요약**

- **`SequencedCollection`**: 순서가 있는 컬렉션(`List`, `Deque`)을 위한 공통 인터페이스 (`getFirst()`, `getLast()` 지원).
- **`SequencedSet`**: 순서를 유지하는 `Set`(`LinkedHashSet`)에서 활용 가능.
- **`SequencedMap`**: 순서를 유지하는 `Map`(`LinkedHashMap`)에서 활용 가능 (`firstEntry()`, `lastEntry()` 등 제공).
- **기존 컬렉션(`ArrayList`, `LinkedList`, `LinkedHashSet`, `LinkedHashMap`)이 자동으로 이 인터페이스를 구현하도록 변경됨.**

---

### **Java 21 `SequencedCollection`의 핵심 변화**

✅ **순서가 있는 컬렉션(`List`, `Set`, `Map`)에서 첫 번째/마지막 요소 접근이 더 쉬워짐**  
✅ **기존 `List`, `LinkedHashSet`, `LinkedHashMap` 등이 자동으로 지원**  
✅ **`reversed()` 메서드로 컬렉션을 쉽게 반전 가능**

**👉 기존의 `List`, `Set`, `Map`을 더 직관적으로 사용할 수 있도록 개선된 기능이라고 보면 됨!**