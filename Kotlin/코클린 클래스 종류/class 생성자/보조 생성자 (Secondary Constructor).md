---
tags: kotlin, secondary, constructor, this, class
---
### 보조 생성자 (Secondary Constructor)

보조 생성자는 클래스 본문 내에서 `constructor` 키워드를 사용하여 선언됩니다. 보조 생성자는 주 생성자와 달리 여러 개 선언할 수 있으며, 다양한 방법으로 객체를 생성할 수 있게 해줍니다. 
```kotlin
class User(val name: String) {
	init { 
		println("주 생성자: 이름은 $name 입니다.") 
	}
    constructor(name: String, age: Int) : this(name) {
        println("보조 생성자: 이름은 $name, 나이는 $age 입니다.")
    }
    constructor(name: String, age: Int, height: Int) : this(name, age){
	    println("보조 생성자: 이름은 $name, 나이는 $age, 키는 $height 입니다.")
    }
    constructor() : this("Unknown") {
        println("보조 생성자: 이름 정보가 없습니다.")
    }
}
```
1단계: 예시 코드의 <mark style="background: #FF5582A6;">주 생성자</mark> 설명 주 생성자는 `User(val name: String)`으로 정의되어 있으며, `name` 매개변수를 받아 클래스의 `name` 프로퍼티를 초기화합니다.

2단계: 예시 코드의 <mark style="background: #FF5582A6;">첫 번째 보조 생성자</mark> 설명 첫 번째 보조 생성자는 `constructor(name: String, age: Int)`로 정의되어 있습니다. 이 생성자는 `name`과 `age` 매개변수를 받고, `this(name)`을 통해 주 생성자를 호출하여 `name` 프로퍼티를 초기화합니다.

3단계: 예시 코드의 <mark style="background: #FF5582A6;">두 번째 보조 생성자</mark> 설명 두 번째 보조 생성자는 `constructor()`로 정의되어 있습니다. 이 생성자는 매개변수가 없으며, `this("Unknown")`을 통해 주 생성자를 호출하여 `name` 프로퍼티를 "Unknown"으로 초기화합니다.

4단계: 주 생성자와 보조 생성자 간의 호출 관계 <mark style="background: #BBFABBA6;">각 보조 생성자는 `this()`를 사용해 주 생성자를 호출</mark>하고 있습니다. 이를 통해 주 생성자에 정의된 초기화 로직을 재사용하고 있습니다.

---
***보조 생성자가 주 생성자를 호출하려면, <mark style="background: #FFB8EBA6;">`this()`를 사용</mark>하여 <mark style="background: #FFB8EBA6;">주 생성자를 명시적으로 호출해야 합니다.</mark>***
- 보조 생성자는 가능하면 적게 사용하는 것이 좋습니다.
- 가능하면 주 생성자를 통한 초기화를 선호하는 것이 좋습니다.
- 생성자에서 너무 많은 로직을 처리하지 않는 것이 좋습니다.
- 여러 보조 생성자가 있는 경우, 코드의 복잡성이 높아질 수 있으므로 주의가 필요합니다.