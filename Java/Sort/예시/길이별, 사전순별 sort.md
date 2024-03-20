---
tags: java, sort, comparator, comparable, 길이순서 정렬, 사전순별, arrays, collections
---
1. **Lambda Expression**: 여기서는 람다 표현식을 사용하여 `Comparator` 인터페이스를 구현합니다.
2. **정렬 기준**:
    - 먼저 두 문자열의 길이를 비교합니다.
    - 길이가 같으면, 문자열들을 사전순으로 비교합니다 (`o1.compareTo(o2)`).
    - 길이가 다르면, 길이의 차이를 기준으로 비교합니다 (`o1.length() - o2.length()`).
```java
import java.util.Arrays;
import java.util.Comparator;
import java.util.Scanner;

class Main {
	public static void main(String args[]) {
		String[] arString = new String[num];

		Arrays.sort(arString, new Comparator<String>() {
			@Override
			public int compare(String o1, String o2) {
				if (o1.length() == o2.length())
					return o1.compareTo(o2);
				else
					return o1.length() - o2.length(); 
			}
		});

		for (int i = 0; i < arString.length; i++) {
			if (i != 0) {
				if (!(arString[i].equals(arString[i - 1])))
					System.out.println(arString[i]);
			}
			else
				System.out.println(arString[i]);
		}
	}
}
```

```java
Collections.sort(combination, (o1, o2) -> {
      if (o1.length() == o2.length())
        return o1.compareTo(o2);
      else
        return o1.length() - o2.length();
    });
    
Collections.sort(combination, Comparable::compareTo);
```
