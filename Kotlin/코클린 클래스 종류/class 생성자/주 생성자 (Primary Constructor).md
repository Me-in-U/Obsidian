---
tags: kotlin, primary, constructor, class
---
주 생성자는 클래스 선언부에 위치하며, 간단한 초기화 작업을 수행할 수 있습니다. 주 생성자는 `constructor` 키워드를 생략할 수 있으며, 클래스 헤더에 직접 매개변수를 선언할 수 있습니다.
```kotlin
class Person(val name: String, var age: Int) {     
	// 클래스 본문 
}
```

이 경우, `Person` 클래스는 이름과 나이 두 개의 속성을 가지며, 이 속성들은 주 생성자를 통해 초기화됩니다.