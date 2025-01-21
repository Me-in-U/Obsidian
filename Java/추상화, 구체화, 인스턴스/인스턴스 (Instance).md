#### **정의**

- 클래스를 기반으로 생성된 **실제 객체**.
- 클래스는 설계도이고, **인스턴스는 설계도로 만든 실제 사물**.

#### **특징**

- 메모리에 실체로 존재하며, 클래스에서 정의된 속성과 동작을 가질 수 있습니다.
- 하나의 클래스에서 여러 개의 인스턴스를 만들 수 있음.

#### **예제**
```java
public class Car {
    String color;
    void drive() {
        System.out.println("차가 달립니다.");
    }
}

public static void main(String[] args) {
    Car car1 = new Car(); // Car 클래스의 인스턴스
    car1.color = "Red";   // car1의 속성 설정

    Car car2 = new Car(); // 또 다른 인스턴스
    car2.color = "Blue";  // car2의 속성 설정
}
```

- `car1`과 `car2`는 `Car` 클래스의 **인스턴스**.
- 서로 다른 데이터를 가지며, 독립적으로 동작합니다.