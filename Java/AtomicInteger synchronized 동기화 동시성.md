---
tags: sync, java
---
## **`synchronized`**

### **정의**

- **스레드 간의 동기화(Synchronization)를 보장**하기 위한 키워드.
- 한 번에 하나의 스레드만 특정 코드 블록 또는 메서드에 접근하도록 제한.

### **특징**

1. **동기화 보장**
    - 한 번에 하나의 스레드만 동기화된 메서드나 블록에 접근 가능.
    - Race Condition 방지.
2. **가시성**
    - `synchronized` 블록 안에서의 변수는 모든 스레드에 **일관된 값을 보장**.
3. **성능 저하**
    - 동기화는 오버헤드가 발생하기 때문에 불필요한 동기화는 피해야 함.

### **사용 사례**

- 중요한 데이터의 읽기/쓰기 작업에서 동기화가 필요할 때.
- 예: Counter, 파일 접근 등.

### **예제**
```java
class Counter {
    private int count = 0;

    public synchronized void increment() { // synchronized 메서드
        count++;
    }

    public synchronized int getCount() {
        return count;
    }
}

public class Main {
    public static void main(String[] args) {
        Counter counter = new Counter();

        Runnable task = () -> {
            for (int i = 0; i < 1000; i++) {
                counter.increment();
            }
        };

        Thread t1 = new Thread(task);
        Thread t2 = new Thread(task);

        t1.start();
        t2.start();

        try {
            t1.join();
            t2.join();
        } catch (InterruptedException e) {
            e.printStackTrace();
        }

        System.out.println("Final count: " + counter.getCount());
    }
}

```

---

## **3. `AtomicInteger`**

### **정의**

- **동기화 없이 원자적(Atomic)으로 정수 값을 다룰 수 있는 클래스**.
- `java.util.concurrent.atomic` 패키지에 포함됨.
- 내부적으로 CAS(Compare-And-Swap) 알고리즘을 사용하여 Lock 없이 동기화 문제를 해결.

### **특징**

1. **원자적 연산(Atomicity)**
    - `incrementAndGet()`, `decrementAndGet()`, `addAndGet()` 등은 한 번에 수행되며 Race Condition이 발생하지 않음.
2. **성능**
    - `synchronized`보다 가볍고 빠름.
    - Lock을 사용하지 않기 때문에 동기화 오버헤드가 적음.
3. **가시성**
    - `volatile`과 마찬가지로 메모리 가시성을 보장.

### **사용 사례**

- 단순한 카운터 또는 값을 원자적으로 업데이트해야 하는 경우.
- 예: 요청 수, 공유 리소스 상태 업데이트.

### **예제**
```java
import java.util.concurrent.atomic.AtomicInteger;

class Counter {
    private AtomicInteger count = new AtomicInteger(0);

    public void increment() {
        count.incrementAndGet(); // 원자적 증가
    }

    public int getCount() {
        return count.get();
    }
}

public class Main {
    public static void main(String[] args) {
        Counter counter = new Counter();

        Runnable task = () -> {
            for (int i = 0; i < 1000; i++) {
                counter.increment();
            }
        };

        Thread t1 = new Thread(task);
        Thread t2 = new Thread(task);

        t1.start();
        t2.start();

        try {
            t1.join();
            t2.join();
        } catch (InterruptedException e) {
            e.printStackTrace();
        }

        System.out.println("Final count: " + counter.getCount());
    }
}

```

| 특징        | volatile         | synchronized             | AtomicInteger      |
| --------- | ---------------- | ------------------------ | ------------------ |
| 기본 목적     | 메모리 가시성 보장       | 원자적 연산과 가시성 보장           | 도익화 없는 원자적 연산      |
| 동기화 방식    | 비동기화             | 동기화(Lock) 사용             | 내부적으로 CAS 알고리즘 사용  |
| 원자적 연산 보장 | X                | O                        | O                  |
| 성능        | 가장 빠름(오버헤드 없음)   | 느림 (Lock 오버헤드 있음)        | 빠름 (동기화 없이 원자성 보장) |
| 사용 사례     | 단순 플래그, 읽기 전용 변수 | 복합 연산(Race Condition) 방지 | 카운터, 원자적 업데이트      |
