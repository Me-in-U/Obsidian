---
tags: kotlin, object, class, Inheritance
---
```kotlin
open class SuperClass{
  open var a : Int? = null
  open fun show(){
    print("no data")
  }
}

val obj = object:SuperClass(){
  override var a :Int? = 1234
  override fun show(){
    println(a)
  }
}

fun main(){
  obj.show()
  val obj2 = object{
    var a = 5678
    fun show(){
      print(a)
    }
  }
  obj2.show()
}
```