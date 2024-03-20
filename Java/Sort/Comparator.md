---
tags: java, sort, comparator
---
## Comparator
1. **정의**: `Comparator` 인터페이스는 정렬을 수행하는 별도의 클래스에 구현됩니다. 이를 통해 여러 가지 정렬 기준을 정의할 수 있습니다.
2. **메서드**: `compare(T o1, T o2)` 메서드를 오버라이드하여 구현합니다. 이 메서드는 두 객체 o1과 o2를 비교합니다.
3. **사용**: 사용자 정의 정렬 기준을 정의하는 데 사용됩니다. `Collections.sort()` 또는 `Arrays.sort()` 메서드와 함께 사용하여 객체들을 정렬할 수 있습니다.
4. **예시**:
``` java
import java.util.Comparator;

public class PersonComparator implements Comparator<Person> {
	@Override     
	public int compare(Person o1, Person o2) {
		return o1.getName().compareTo(o2.getName());     
	} 
}
```

`Comparator` 인터페이스를 구현할 때, `compare` 메서드를 오버라이드하여 두 객체를 비교하는 로직을 정의해야 합니다. 여기서 `compareTo` 메서드는 `String` 클래스에 정의된 메서드로, 문자열을 사전순으로 비교하는데 사용됩니다.

코드에서 `o1.getName()`과 `o2.getName()`은 각각 `Person` 객체의 이름을 반환하는 메서드입니다. 이 이름들은 `String` 타입이므로, `compareTo` 메서드를 사용하여 사전순으로 비교할 수 있습니다.

따라서, `Comparator`의 `compare` 메서드 내에서 `compareTo` 메서드를 사용하는 것은, 두 `Person` 객체의 이름을 사전순으로 비교하기 위함입니다.
