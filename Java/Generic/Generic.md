---
tags:
  - java
  - generic
---
**Generic(제네릭)**은 자바에서 클래스나 메서드가 *사용할 데이터 타입을 컴파일 시에 지정할 수 있도록 하는 기능*입니다. 컬렉션(List, Set, Map 등)이나 기타 클래스에서 타입 안정성(type safety)을 높이고, 형 변환(casting)을 최소화하기 위해 사용됩니다.

### **Generic을 사용하는 이유 (요약)**
1. **타입 안정성 확보** → 잘못된 타입 사용을 **컴파일 시점에 방지**
2. **형 변환 불필요** → `Object`로 저장 후 꺼낼 때 **캐스팅이 필요 없음**
3. **코드 재사용성 증가** → **다양한 타입을 처리하는 범용 코드 작성 가능**
4. **가독성 및 유지보수 향상** → **타입 명확성 증가, 오류 발생 가능성 감소**

- 제네릭을 사용하지 않은 경우 (형 변환 필요)
```java
import java.util.*;

public class NonGenericExample {
    public static void main(String[] args) {
        List list = new ArrayList();
        list.add("Hello");
        list.add(10);  // 잘못된 타입이 들어가도 컴파일 에러 없음

        String str = (String) list.get(0); // 형 변환 필요
        System.out.println(str);
    }
}
```
> 단점: `list.add(10);`이 가능하며, 실행 시 `ClassCastException` 발생 가능

- 제네릭을 사용한 경우 (형 변환 불필요)
```java
import java.util.*;

public class GenericExample {
    public static void main(String[] args) {
        List<String> list = new ArrayList<>(); // 타입 지정
        list.add("Hello");
        // list.add(10);  // 컴파일 에러 발생 (잘못된 타입 추가 방지)

        String str = list.get(0); // 형 변환 없이 바로 사용 가능
        System.out.println(str);
    }
}
```
>장점: **컴파일 시 타입 검사가 이루어져 오류를 방지**하고, **형 변환이 필요 없음**

### 제네릭을 활용한 클래스 예제
```java
// 제네릭 클래스 선언
class Box<T> {
    private T item;

    public void setItem(T item) {
        this.item = item;
    }

    public T getItem() {
        return item;
    }
}

public class GenericClassExample {
    public static void main(String[] args) {
        Box<String> stringBox = new Box<>();
        stringBox.setItem("Hello, Generic!");
        System.out.println(stringBox.getItem());

        Box<Integer> intBox = new Box<>();
        intBox.setItem(123);
        System.out.println(intBox.getItem());
    }
}

```