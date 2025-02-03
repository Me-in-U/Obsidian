---
tags: java, sealed, class
---
- 봉인된 클래스로 내가 관리하는 특정 클래스에게만 상속 가능
- 상속 계층 내에서 엄격한 제어를 통해
	- 프로그램의 구조를 명확하게 유지하고 의도치 않은 상속으로 인한 복잡성과 혼방지
	- 명확한 역할과 직무 분류가 중요한 개념에서 주로 사용

### 작성법
- class(interface 포함)에 sealed 키워드를 사용하고 상속(구현)을 허락하느 클래스를 permits뒤에 나열해줌
	- sealed가 선언된 클래스는 permits가 반드시 필요
- 구현 클래스는 다음 키워드 중 하나 사용 필요
	- sealed: 여전히 봉인된 클래스로 추가적을 permits로 하위 클래스 나열 필요
	- final: 더 이상 상속 받을 수 없는 클래스
	- non-sealed: 봉인이 해제된 클래스로 자유롭게 상속 가능

Sealed 클래스는 상속 제한을 위해서 도입됐다. 이 역시 코들린에 비슷한 기능이 있고 생각해보니 자바에서 신규 지원하는 많은 기능들이 코틀린에서 사용하는것 같다. 기존의 자바에서 상속 금지를 위해서 아래와 같이 약간의 기교(?)를 부려야 했다.
```java
public final class Member {
 private Member() {
  //no constuctor
 }
}
```

Sealed class 를 이용한 상속제한
```java
public static sealed abstract class Bird permits Sparrow, Penguin {
    public abstract void fly();
}

public static final class Sparrow extends Bird {
    @Override
    public void fly() {
        System.out.println("Sparrow fly");
    }
}

public static final class Penguin extends Bird {
    @Override
    public void fly() {
        System.out.println("Penguin can't fly");
    }
}
public static final class Tiger extends Bird { //compile error: 'Tiger' is not allowed in the sealed hierarchy
    @Override
    public void fly() {
        
    }
}
```
인터페이스에서도 동일하게 사용가능하면 한가지 지켜야할 점은 점은 상속받는 클래스들 역시 반드시 final, sealed, non-sealed 세가지 키워드중 한 개를 사용해야 된다. 상속 받은 클래스(위 예제에서 Sparrow, Penguin) 들 역시 부모 클래스가 될 수 있기 때문에 제약성을 유지할지 아니면  상속 금지를 할지를 정해야 된다.(make sense하다.) 아래는 관련된 예시이다.

```java
public static sealed class Sparrow  extends Bird permits KingSparrow {
    @Override
    public void fly() {
        System.out.println("Sparrow fly");
    }
}

public static non-sealed class Penguin extends Bird {
    @Override
    public void fly() {
        System.out.println("Sparrow fly");
    }
}

//Penguin non-sealed 이기 때문에 어떤한 클래스도 상속 가능
public static final class NorthPerson extends Penguin {
    public void fly(Bird bird) {
        bird.fly();
    }
}

public static final class KingSparrow extends Sparrow {
    public void fly(Bird bird) {
        bird.fly();
    }
}
//Sparrow 는 sealed class 로 KingSparrow 만 상속 가능하다.
public static final class NorthPerson extends Sparrow { //compile error 
    public void fly(Bird bird) {
        bird.fly();
    }
}
```