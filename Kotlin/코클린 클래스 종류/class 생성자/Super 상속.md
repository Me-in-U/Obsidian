---
tags: kotlin, super, Inheritance, class
---
- 매개변수가 있는 상위 클래스의 생성자 호출
- 주 생성자를 통해 상위 클래스의 생성자를 호출
```kotlin
open class Super(name: String) {
}
class Sub(name: String): Super(name) {
}
```

- 하위 클래스에 보조 생성자만 있는 경우 상위 클래스의 생성자 호출
- 보조 생성자를 통해 상위 클래스의 생성자를 호출
```kotlin
open class Super(name: String) {
}
class Sub: Super {
	constructor(name: String): super(name) {
	}
}
```

``` kotlin
open class Super {
	open var someData = 10
	open fun someFun() {
		println("i am super class function :$someData")
	}
}
class Sub: Super() {
	override var someData = 20
	override fun someFun() {
		println("i am sub class function : $someData")
	}
}

fun main() {
	val obj = Sub()
	obj.someFun()
}
```
>실행 결과
>i am sub class function : 20