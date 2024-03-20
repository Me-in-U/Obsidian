---
tags:
  - kotlin
  - class
  - constructor
---
코틀린에서 생성자가 없는 클래스는 주로 <mark style="background: #FF5582A6;">데이터를 저장</mark>하거나 <mark style="background: #FF5582A6;">단순한 연산</mark>을 수행하는 용도로 사용됩니다. 주 생성자가 명시적으로 정의되어 있지 않은 경우, 컴파일러는 암시적으로 <mark style="background: #ABF7F7A6;">빈 생성자를 제공</mark>합니다.

#### 주의사항과 팁
- 생성자가 없는 클래스는 상태가 없거나, 상태 초기화에 필요한 로직이 없을 때 주로 사용됩니다.

#### 사용 사례
- DTO(Data Transfer Object), 싱글턴 패턴, 유틸리티 클래스 등
```kotlin
class User{
	var name = "kkang"
	constructor(name: String){
		this.name = name
	}
	fun someFun(){
		println("name :" $name)
	}
	class SomeClass{}
}
```
---
