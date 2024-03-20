---
tags: kotlin, data, class
---
1. 데이터를 보관하는 목적으로 사용되는 클래스입니다. 
2. VO 클래스를 편리하게 이용할 수 있는 방법 제공
## 주요 특징:
### `equals()`: 객체의 내용이 같은지 비교
- 두 객체의 내용이 동일한지 비교하는 메서드입니다
- 이 메서드는 객체의 모든 프로퍼티를 비교하여 두 객체가 동일한지 확인합니다.

#### 작동 원리:
1. **Type Check**: 먼저, 두 객체의 타입이 동일한지 확인합니다.
2. **Null Check**: `null`과 비교할 경우, `equals()`는 `false`를 반환합니다.
3. **Property Comparison**: 주 생성자에 선언된 모든 프로퍼티를 비교합니다. 모든 프로퍼티가 동일하면 `true`를 반환하고, 그렇지 않으면 `false`를 반환합니다.
```kotlin
data class DataClass(val name: String, val email: String, val age: Int) {
    lateinit var address: String
    constructor(name: String, email: String, age: Int, address: String) : this(name, email, age) {
        this.address = address
    }
}

fun main() {
    val obj1 = DataClass("kkang", "A@a.com", 10, "Seoul")
    val obj2 = DataClass("kkang", "A@a.com", 10, "Busan")
    println("obj1.equals(obj2): ${obj1 == obj2}") 
}
```
위 코드에서 `obj1`과 `obj2`는 주 생성자에 선언된 `name`, `email`, `age`가 동일하므로 `equals()`는 `true`를 반환합니다. `address`는 비교 대상에서 제외됩니다.
-><mark style="background: #FFB8EBA6;"> 주 생성자에 선언한 멤버 변수의 데이터만 비교대상</mark>

### Equlas 구현된 방
```kotlin
data class Person(val name: String, val age: Int)

override fun equals(other: Any?): Boolean {
    if (this === other) return true // 첫 번째 검사: 참조 동등성
    if (javaClass != other?.javaClass) return false // 두 번째 검사: 같은 클래스인지 확인

    other as Person

    if (name != other.name) return false // 세 번째 검사: 각 필드가 동일한지 확인
    if (age != other.age) return false

    return true // 모든 검사를 통과했으면, 객체는 동등합니다.
}
```
### `toString()`: 객체를 문자열로 표현
- 이 메서드는 주 생성자에 선언된 프로퍼티만을 포함하여 문자열을 생성합니다.
- 예를 들어, 다음과 같은 `data class`가 있다고 가정해봅시다.

```kotlin
data class Person(val name: String, val age: Int) {
    var address: String = "Unknown"
}
```
이 경우, `toString()` 메서드는 다음과 같이 작동합니다:
```kotlin
fun main() {
    val person = Person("John", 30)
    person.address = "New York"
    println(person.toString())  // 출력: "Person(name=John, age=30)"
}
```
주목할 점은 `address` 프로퍼티가 `toString()`의 결과에 포함되지 않는다는 것입니다. 이는 `address`가 주 생성자에 선언되지 않았기 때문입니다.


### `hashCode()`: 객체의 해시 코드 생성

### `copy()`: 객체 복사

### `componentN()`: 객체의 속성을 분해


