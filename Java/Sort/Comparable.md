---
tags: java, sort, comparable
---
## Comparable

1. **정의**: `Comparable` 인터페이스는 정렬을 수행하는 클래스 내부에 구현됩니다. 클래스가 자신의 인스턴스들을 어떻게 비교할지 정의합니다.
2. **메서드**: `compareTo(T o)` 메서드를 오버라이드하여 구현합니다. 이 메서드는 현재 객체와 매개변수로 전달된 객체를 비교합니다.
3. **사용**: 일반적으로 자연적인 순서로 정렬하는 데 사용됩니다.
4. **예시**:
``` java
public class Person implements Comparable<Person> {
	private String name; 
	@Override     
	public int compareTo(Person o) { 
		return this.name.compareTo(o.name);   
	}
}
```
