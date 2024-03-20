---
tags: kotlin, 변수, 지연, 초기화, lateinit
---
`lateinit`은 코틀린에서 <mark style="background: #ADCCFFA6;">지연 초기화</mark>를 위한 키워드입니다. 일반적으로 클래스의 프로퍼티를 선언할 때 초기값을 할당해야 합니다. 그러나 경우에 따라 프로퍼티의 초기값이 나중에 (예: 생성자 이후의 시점에) 결정되어야 할 수 있습니다. 이러한 경우 `lateinit` 키워드를 사용하여 프로퍼티를 지연 초기화할 수 있습니다.

다음은 `lateinit`의 몇 가지 주요 특징 및 사용 방법에 대한 설명입니다:

### 기본 사용법
`lateinit` 키워드는 클래스의 프로퍼티 선언에 사용됩니다. 이 키워드는 프로퍼티가 나중에 초기화될 것임을 나타냅니다.
```kotlin
class MyActivity {    
	lateinit var name: String 
}
```

### 초기화
`lateinit`으로 선언된 프로퍼티는 나중에 초기화할 수 있습니다. 이 초기화는 생성자 이외의 메서드에서 수행할 수 있습니다.

```kotlin
class MyActivity {  
	lateinit var name: String    
	fun init(name: String) {   
		this.name = name  
	} 
}
```

### 제한 사항
- `lateinit`은 `val` (읽기 전용 프로퍼티)에 사용할 수 없으며, `var` (가변 프로퍼티)에만 사용할 수 있습니다.
- `lateinit` 프로퍼티는 기본 자료형 (Int, Double 등)에 사용할 수 없습니다. 참조 형식에만 사용할 수 있습니다.
- `lateinit` 프로퍼티는 커스텀 getter/setter를 가질 수 없습니다.

### 초기화 확인
`lateinit` 프로퍼티가 이미 초기화되었는지 확인하려면 `::` 연산자와 `isInitialized` 속성을 사용할 수 있습니다.

```kotlin
if (::name.isInitialized) {   
	println("Name is initialized") 
}
```

### 사용 사례
`lateinit`은 주로 의존성 주입 또는 단위 테스트에서 모크 객체를 주입할 때 사용됩니다. 또한 Android에서 뷰 바인딩 또는 프래그먼트와 액티비티 간의 인터페이스 통신에도 사용됩니다.

이러한 방법으로, `lateinit` 키워드는 코틀린에서 지연 초기화를 수행하는 강력한 도구로 작용합니다, 그러나 <mark style="background: #FF5582A6;">초기화되지 않은 상태에서 접근하려고 하면 런타임 예외가 발생하므로 주의가 필요합니다.</mark>