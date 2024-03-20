---
tags: java, list, LinkedList, ArrayList, Vector, Queue, Deque, Stack, collections
---
[자바에서 Vector와 Stack 컬렉션이 쓰이지 않는 이유?](https://aahc.tistory.com/8)

자바에서 Deque를 구현하는 방법은 크게 LinkedList와 ArrayDeque가 있는데, 스택의 size가 엄청 커질 가능성이 있고 size의 변동성이 매우 큰 경우 즉각적인 메모리 공간 확보를 위해선 LinkedList방식이 적절하고, 그렇지 않은 경우는 자체 메모리 소모량이 적고 iterate의 효율이 좋은 ArrayDeque를 사용하면 된다.

### **뭘 써야할까**
Java의 Vector와 Stack은 멀티스레드 환경의 여부와 상관없이 대부분의 조건에서 성능 저하를 일으킨다.

Vector가 필요한 상황이라면 대신 ArrayList를 사용하는 것이 바람직하다.

마찬가지로 Stack 대신 Deque의 하위컬렉션을 상황에 맞게, 혹은 그냥 ArrayList를 사용하는 것이 적절하다.

- 순차적으로 데이터를 추가/삭제 => ArrayList가 빠름
  (뒤에 데이터를 넣을 때)
- 비 순차적으로 데이터를 추가/삭제 => LinkedList가 빠름
  (앞에 넣거나 데이터 추가 삭제 변경이 빈번할 때)
- 접근 시간, 검색 시간 => ArrayList가 빠름

### 장단점
#### ArrayList
- 저장용량을 초과한 객체가 들어오면 자동으로 저장용량이 늘어납니다.
 - 타임 파라미터 표기
 - 기본 생성자로 객체를 생성하면 객체 10개를 저장할 수 있는 초기 용량을 가지게 됩니다.
 - 하지만 객체수가 늘어나면 용량이 자동으로 증가합니다.
 - 객체를 추가하면 인덱스 0부터 차례대로 저장됩니다.
 - 특정 인덱스의 객체를 제거하면 바로 뒤의 인덱스부터 끝까지 모두 1씩 당겨지게 됩니다.
	 - **장점** : 인덱스 검색이나 마지막에 객체를 추가할 때 좋은 성능을 냅니다.
	- **단점** : 빈번한 객체 삭제와 삽입이 일어나는 곳에서 사용하기 힘듭니다.

#### LinkedList
- 어레이 리스트와 사용 방법은 같지만 내부 구조가 전혀 다릅니다.
- 특정 인덱스의 객체를 제거하면 앞뒤 링크만 변경되고, 나머지는 변경되지 않습니다.
	- **장점** : 빈번한 객체 추가와 삭제가 일어나는 곳에서 사용하기 좋습니다.
	- **단점** : 순차적으로 객체 추가 삭제와 검색하는 속도가 느립니다.

## 코드 예제

```java
import java.util.ArrayList;
import java.util.LinkedList;
import java.util.List;
import java.util.Vector;
```
### 선언
```java
ArrayList<String> list = new ArrayList<>();
LinkedList<String> list = new LinkedList<>();
Vector<String> list = new Vector<>();
```
### Stack(Last In First Out)
```java
import java.util.Stack;

Stack<String> list = new Stack<>(); 
```
#### <데이터 추가>
``` java
//최상단 데이터 추가
<데이터 추가> boolean add(Object o)
//최상단 데이터 추가 <데이터 제거&&반환리턴>
Object push(Object item);
```
#### <데이터 제거&&반환리턴>
``` java
//최상단 데이터 출력(제거 x)
Object peek();
//최상단 데이터 꺼내기
Object pop();
```
#### <기타>
``` java
//모든 데이터 삭제 size() == 0
stk.clear();
//비어있는지 확인
boolean isEmpty
//최상단 ==1 못찾으면 -1
int search(Object ite m)
```


### Queue(First In First Out)
-  Queue는 인터페이스여서 new Queue 객체생성 블가능
``` java
import java.util.Queue;
import java.util.LinkedList;

Queue<Character> queue = new LinkedList<>();
```
#### <데이터 추가>
``` java
//가장 뒤 데이터 추가 (큐 공간 없으면 EmptyStackException)
boolean add(Object o)
//가장 뒤 데이터 추가 (큐 공간 없으면 False)
boolean offer(Object o)
```
#### <데이터 제거&&반환리턴>
``` java
//가장 앞 데이터 반환/삭제
Object poll()
//가장 앞 데이터 반환
Object peek()
//삭제없이 요소 읽기( (비어있으면 NoSuchElementException 반환)
Object element()
//객체를 꺼내 반환 (비어있으면 NoSuchElementException 반환)
Object remove()
```

### Deque
``` java
import java.util.Deque;
import java.util.ArrayDeque;
Deque<Integer> dq = new ArrayDeque<>();
```
#### <데이터 추가>
```java
//가장 앞/"뒤" 데이터 추가 (큐 공간 없으면 EmptyStackException)
Object addFirst/Last();
//가장 앞/"뒤"에 데이터 추가 (큐 공간 없으면 False)
boolean offerFirst/Last();
```
#### <데이터 제거>
```java
//가장 "앞"/뒤 원소 제거후 반환 (비어있으면 예외 발생) 
removeFirst/Last();
//가장 "앞"/뒤 데이터 제거 후 반환 (비어있으면 null리턴)
pollFirst/last();
```
#### <원소확인>
``` java
//맨 앞/뒤 원소를 반환 (비어있으면 예외 발생)
getFirst/Last();
//가장 "앞"/뒤 데이터 반환 (덱이 비어있으면 null 리턴)
peekFirst/Last();
```
#### <기타>
```java
//덱의 맨 앞/뒤에서 시작에서 x와 동일한 첫 원소를 제거 First== remove(x)
removeFirst.LastOccurrence(x);
```

### LinkedList 클래스 주요 메서드
- **add** : *해당 큐의 맨 뒤에 전달된 요소를 삽입합니다*
- **element** : *해당 큐의 맨 앞에 있는(제일 먼저 저장된) 요소를 반환합니다*
- **offer** : *해당 큐의 맨 뒤에 전달된 요소를 삽입합니다*
- **peek** : *해당 큐의 맨 앞에 있는(제일 먼저 저장된) 요소를 반환합니다*
- **poll** : *해당 큐의 맨 앞에 있는(제일 먼저 저장된) 요소를 반환하고, 해당 요소를 큐에서 제거합니다*
- **remove** : *해당 큐의 맨 앞에 있는(제일 먼저 저장된) 요소를 제거합니다*
- **size** : *해당 큐의 크기 (사이즈) 를 구합니다*
- **clear** : *해당 큐에 저장된 데이터를 전체 삭제합니다*

### List 클래스 주요 메서드
```java
boolean add(E e);
//밀림
void add(int index, E element);
//인덱스를 통한 조회
E get(int index);
//동일한 오브젝트로 삭제하기 return(true/false)
boolean remove(Object o);
// 인덱스로 삭제하기 return(삭제한 결과값)
E remove(int index); 
// 포함 여부 확인 return(true/false)
boolean contains(Object o);
void clear(); 
int size(); 
isEmpty(); 
int index = values.indexOf(item);
```

