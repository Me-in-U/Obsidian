---
tags: class, kotlin, init
---
코틀린에서는 `init` 블록을 통해 생성자에서 추가적인 초기화 작업을 수행할 수 있습니다. `init` 블록은 클래스가 인스턴스화될 때 실행되며, 주 생성자와 함께 작동합니다.
```kotlin
class Person(val name: String, var age: Int) {
    init { println("Person 인스턴스가 생성되었습니다. 이름은 $name, 나이는 $age 입니다.")
	}
}
```
- `init` 블록은 클래스에 여러 개 있을 수 있으며, 선언된 순서대로 실행됩니다.
- `init` 블록 내에서는 주 생성자의 매개변수에 접근할 수 있습니다.
---
### 객체 생성 예시
``` kotlin
fun main(){
	val person = Person("이름", 24)
}
```