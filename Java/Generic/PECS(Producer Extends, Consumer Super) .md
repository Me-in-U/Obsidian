---
tags: java, pecs
---
### **📌 PECS(Producer Extends, Consumer Super) 원칙이 필요한 이유**

PECS 원칙은 **제네릭 와일드카드 사용 시 데이터의 "읽기"와 "쓰기"를 올바르게 처리하기 위한 규칙**입니다.

- **Producer는 `extends`를 사용한다.** (`? extends T`) → 데이터를 "읽기"만 가능
- **Consumer는 `super`를 사용한다.** (`? super T`) → 데이터를 "쓰기"만 가능

즉, **읽을 때는 하위 타입까지 허용하고, 쓸 때는 상위 타입까지 허용**해야 **타입 안정성을 유지**할 수 있습니다.

---

## **📌 PECS가 필요한 이유 및 예제 코드**

### **1️⃣ `? extends T` → 데이터를 "읽기"만 가능 (Producer)**

```java
import java.util.List;

class PECSExample {
    // ✅ `? extends Number`는 "Producer" → 데이터를 가져올 수만 있음 (읽기 전용)
    public static double sumList(List<? extends Number> list) {
        double sum = 0;
        for (Number num : list) { // `Number`로 안전하게 읽을 수 있음
            sum += num.doubleValue();
        }
        return sum;
    }
}

public class Main {
    public static void main(String[] args) {
        List<Integer> intList = List.of(1, 2, 3);
        List<Double> doubleList = List.of(1.1, 2.2, 3.3);

        System.out.println(PECSExample.sumList(intList));   // ✅ 정상 동작 (6.0)
        System.out.println(PECSExample.sumList(doubleList)); // ✅ 정상 동작 (6.6)
        
        // list.add(10); // ❌ 컴파일 에러 (쓰기 불가능)
    }
}
```

> ✅ **이점:** `? extends Number`를 사용하면 `List<Integer>`, `List<Double>` 등 여러 하위 타입을 받을 수 있음.  
> ❌ **제한:** `list.add(T item);`을 할 수 없음 → **타입 안전성을 보장하기 위해 읽기 전용**

---

### **2️⃣ `? super T` → 데이터를 "쓰기"만 가능 (Consumer)**

```java
import java.util.List;
import java.util.ArrayList;

class PECSExample {
    // ✅ `? super Integer`는 "Consumer" → 데이터를 추가할 수 있음 (쓰기 전용)
    public static void addNumbers(List<? super Integer> list) {
        list.add(10);
        list.add(20);
    }
}

public class Main {
    public static void main(String[] args) {
        List<Number> numberList = new ArrayList<>();
        List<Object> objectList = new ArrayList<>();

        PECSExample.addNumbers(numberList); // ✅ 정상 동작
        PECSExample.addNumbers(objectList); // ✅ 정상 동작
        
        // Integer num = numberList.get(0); // ❌ 컴파일 에러 (읽기 불가능)
    }
}
```

> ✅ **이점:** `? super Integer`를 사용하면 `List<Integer>`, `List<Number>`, `List<Object>`까지 받을 수 있음.  
> ❌ **제한:** `list.get(int index);`를 호출할 경우, 반환 타입이 `Object`로 나오므로 직접적인 `Integer` 사용 불가능.

---

## **📌 🚀 PECS 원칙 요약**

|**사용 방식**|**키워드**|**설명**|**예제**|
|---|---|---|---|
|**Producer (읽기 전용)**|`? extends T`|"읽기 전용"으로 사용|`List<? extends Number>`|
|**Consumer (쓰기 전용)**|`? super T`|"쓰기 전용"으로 사용|`List<? super Integer>`|

✅ **읽기 전용(Producer) → `extends` 사용 (하위 타입까지 허용)**  
✅ **쓰기 전용(Consumer) → `super` 사용 (상위 타입까지 허용)**

> **PECS 원칙을 따르면, 제네릭 컬렉션에서 타입 안정성을 유지하면서 "읽기"와 "쓰기"를 구분할 수 있음!** 🚀