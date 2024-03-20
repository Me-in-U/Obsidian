---
tags: 길이순서 정렬, java, sort, comparator, 오름차순, collections
---
```java
Collections.sort(strings, new Comparator<String>() {
	@Override
	public int compare(Strng s1, String s2) {
		return s1.length() - s2.length();
		}
	}
);
```