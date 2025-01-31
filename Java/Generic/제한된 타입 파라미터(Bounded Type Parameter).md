---
tags: java, type, parameter, extends, super
---
### **📌 제한된 타입 파라미터(Bounded Type Parameter)가 필요한 이유**

제네릭 타입 파라미터는 기본적으로 모든 타입(`Object`)을 허용하지만, 특정 타입의 **상위 클래스나 인터페이스를 제한(Bounding)** 하면 더 **안전하고 유용한 코드**를 작성할 수 있습니다.

---
### **📌 제한된 타입 파라미터를 사용하는 이유**

1. **특정 기능을 보장하기 위해**
    - 예를 들어, `Number` 또는 특정 인터페이스를 구현한 타입만 허용하여 **연산이 가능한 타입만 사용하도록 제한** 가능.
    - `T extends Number` → `Integer`, `Double`, `Float` 등만 허용.
2. **타입 안정성(Type Safety) 확보**
    - 타입 제한을 걸어 **잘못된 타입 사용을 컴파일 시점에 방지**.
    - 예: 숫자 연산을 수행해야 하는데, `String`이 들어오는 실수를 방지.
3. **불필요한 캐스팅 방지**
    - 특정 인터페이스를 구현한 타입만 허용하면, **인터페이스의 메소드들을 안전하게 호출 가능**.
    - 예: `T extends Comparable<T>`로 제한하면, `compareTo` 메서드를 바로 사용할 수 있음.

---

### **📌 제한된 타입 파라미터 사용법**

#### **1️⃣ 기본적인 제한 (`extends` 사용)**
```java
// Number를 상속받은 타입만 허용
class Box<T extends Number> {
    private T item;

    public void setItem(T item) {
        this.item = item;
    }

    public T getItem() {
        return item;
    }

    // 숫자 연산 수행 가능 (컴파일 시 안전 보장)
    public double multiplyByTwo() {
        return item.doubleValue() * 2;
    }
}

public class Main {
    public static void main(String[] args) {
        Box<Integer> intBox = new Box<>();
        intBox.setItem(10);
        System.out.println(intBox.multiplyByTwo()); // 20.0

        Box<Double> doubleBox = new Box<>();
        doubleBox.setItem(5.5);
        System.out.println(doubleBox.multiplyByTwo()); // 11.0

        // Box<String> strBox = new Box<>(); // ❌ 컴파일 에러 (String은 Number를 상속하지 않음)
    }
}
```

> ✅ `T extends Number` 덕분에 `doubleValue()` 등의 메소드 사용 가능  
> ✅ `Box<String>`은 허용되지 않음 → **불필요한 타입 오류 방지**
---

#### **2️⃣ 여러 개의 제한 조건 적용 (`&` 연산자 사용)**
```java
// T는 Number를 상속받고, Comparable<T> 인터페이스를 구현해야 함
class DataProcessor<T extends Number & Comparable<T>> {
    private T data;

    public DataProcessor(T data) {
        this.data = data;
    }

    public boolean isGreaterThan(T other) {
        return data.compareTo(other) > 0; // compareTo 사용 가능
    }
}

public class Main {
    public static void main(String[] args) {
        DataProcessor<Integer> intProcessor = new DataProcessor<>(10);
        System.out.println(intProcessor.isGreaterThan(5)); // true

        DataProcessor<Double> doubleProcessor = new DataProcessor<>(7.5);
        System.out.println(doubleProcessor.isGreaterThan(10.0)); // false

        // DataProcessor<String> strProcessor = new DataProcessor<>("Hello"); // ❌ 컴파일 에러 (String은 Number가 아님)
    }
}
```

> ✅ `T extends Number & Comparable<T>` 덕분에 `compareTo()` 메소드 사용 가능  
> ✅ 숫자 타입만 허용되므로, 불필요한 예외 발생 가능성을 제거
---

### **🚀 결론 요약**

|**이점**|**설명**|
|---|---|
|**특정 기능 보장**|연산 가능한 `Number` 타입만 허용 가능|
|**타입 안정성 향상**|잘못된 타입 사용을 **컴파일 시점에 차단**|
|**불필요한 형 변환 방지**|`Comparable<T>` 등 인터페이스 구현 타입을 보장하여 안전한 메소드 호출 가능|
|**코드 재사용성 증가**|다양한 타입을 지원하면서도, **불필요한 타입 제한을 최소화** 가능|

> ✅ **제네릭의 강력한 타입 제한을 활용하면, 안전하고 유연한 코드 작성 가능!** 🚀