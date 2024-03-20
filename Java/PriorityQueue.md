---
tags: java, Queue, PriorityQueue, sort, 내림차순, 오름차순, heap
---
# 선언
```java
import java.util.PriorityQueue; 

// E형 priorityQueue 선언 (우선순위가 낮은 숫자 순)
PriorityQueue<E> priorityQueue = new PriorityQueue<>();
// E형 priorityQueue 선언 (우선순위가 높은 숫자 순)
PriorityQueue<E> priorityQueue = new PriorityQueue<>(Collections.reverseOrder());
```
## 값 추가
``` java
priorityQueue.add(1);
priorityQueue.add(2);
priorityQueue.offer(3);
```
## 값 삭제
```java
priorityQueue.poll();       // priorityQueue에 첫번째 값을 반환하고 제거 비어있다면 null
priorityQueue.remove();     // priorityQueue에 첫번째 값 제거
priorityQueue.clear();      // priorityQueue에 초기화
```
## 우선순위가 가장 높은 값 출력
``` java
priorityQueue.peek();
```

# 우선순위 큐의 특징

1. 높은 우선순위의 요소를 먼저 꺼내서 처리하는 구조 (큐에 들어가는 원소는 비교가 가능한 기준이 있어야함)
2. 내부 요소는 힙으로 구성되어 이진트리 구조로 이루어져 있음
3. 내부구조가 힙으로 구성되어 있기에 시간 복잡도는 O(NLogN)