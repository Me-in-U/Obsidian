객체의 타입을 비교하기 위한 문법이다.
이 또한 코틀린에 해당 기능이 있고 형 체크와 변환을 동시에 할 수 있는 유용한 기능이다.
```java
//as-is
Flyable f1 = new Bird();
Flyable f2 = new Plane();

if (f1 instanceof Bird) {
    Bird b = (Bird) f1;
    b.fly();
}

//java 16+
Flyable f1 = new Bird();
Flyable f2 = new Plane();

if (f1 instanceof Bird b) {
    b.fly();
}
```