---
tags: wildcard, java, extends, super
---
### **📌 와일드카드(Wildcard)가 필요한 이유**

와일드카드는 제네릭 타입을 **보다 유연하게 사용**하기 위해 필요합니다.  
제네릭은 기본적으로 **불공변(invariant)** 하기 때문에, 특정 타입의 하위 클래스라도 **다른 제네릭 타입으로 간주되지 않음**.  
이를 해결하기 위해 `?` 와일드카드를 사용하여 **다양한 타입을 수용할 수 있도록** 합니다.

---

### **📌 와일드카드(`?`)가 없다면 발생하는 문제**

#### **1️⃣ 하위 타입을 포함하는 메서드 사용 불가**

```java
class Box<T> {
    private T item;
    public void setItem(T item) { this.item = item; }
    public T getItem() { return item; }
}

public class Main {
    public static void main(String[] args) {
        Box<Number> numBox = new Box<>();
        Box<Integer> intBox = new Box<>();

        numBox = intBox; // ❌ 컴파일 에러 (불공변성)
    }
}
```

> `Box<Integer>`는 `Box<Number>`의 하위 타입이 아니므로 대입 불가능  
> **💡 해결 방법:** `Box<? extends Number>` 사용
---

#### **2️⃣ 메서드에서 다양한 타입을 처리할 수 없음**

```java
class Util {
    public static void printBox(Box<Number> box) { 
        System.out.println(box.getItem()); 
    }
}

public class Main {
    public static void main(String[] args) {
        Box<Integer> intBox = new Box<>();
        intBox.setItem(10);

        Util.printBox(intBox); // ❌ 컴파일 에러
    }
}
```

> `printBox(Box<Number>)`는 `Box<Integer>`를 받을 수 없음  
> **💡 해결 방법:** `printBox(Box<? extends Number>)` 사용
---

### **📌 와일드카드가 필요한 이유**

#### **1️⃣ 하위 타입을 포함할 수 있도록 (`? extends T`)**

```java
class Util {
    public static void printBox(Box<? extends Number> box) {
        System.out.println(box.getItem()); 
    }
}

public class Main {
    public static void main(String[] args) {
        Box<Integer> intBox = new Box<>();
        intBox.setItem(10);

        Util.printBox(intBox); // ✅ 정상 실행
    }
}
```

> ✅ `? extends Number`를 사용하면 `Box<Integer>`, `Box<Double>` 등 모든 `Number`의 하위 타입을 허용
---

#### **2️⃣ 슈퍼타입을 포함할 수 있도록 (`? super T`)**

```java
class Util {
    public static void addNumber(Box<? super Integer> box) {
        box.setItem(100);
    }
}

public class Main {
    public static void main(String[] args) {
        Box<Number> numBox = new Box<>();
        Box<Object> objBox = new Box<>();

        Util.addNumber(numBox); // ✅ 정상 실행
        Util.addNumber(objBox); // ✅ 정상 실행
    }
}
```

> ✅ `? super Integer`를 사용하면 `Box<Number>`, `Box<Object>` 등 **Integer의 부모 타입**을 허용  
> → **하위 타입을 추가할 때 유용**

---

### **🚀 와일드카드(`?`)가 없다면 생기는 문제 요약**

|**문제점**|**설명**|**해결 방법**|
|---|---|---|
|**제네릭이 불공변이라 하위 타입을 대입할 수 없음**|`Box<Integer>`는 `Box<Number>`로 간주되지 않음|`? extends T` 사용|
|**메서드에서 다양한 제네릭 타입을 받지 못함**|`Box<Number>`만 받도록 선언하면 `Box<Integer>`를 처리할 수 없음|`? extends T` 사용|
|**하위 타입을 추가할 수 없음**|`setItem(T item)`이 특정 타입만 받도록 제한됨|`? super T` 사용|

✅ **결론:** 와일드카드를 사용하면 제네릭 타입을 더 유연하게 활용할 수 있음. 🚀