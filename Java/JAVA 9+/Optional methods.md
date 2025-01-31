---
tags: java, optional
---
자바 8 에서 처음 소개된 Opitonal 은 null 에대한 처리를 좀 더 세련되게 처리 할 수 있다. feature 가 소개된 이후 활용도가 굉장히 높다.8 이후 버전에서 유용한 메서들이 추가 됐다. 아래는 예시이다.
```java
public class Main {
    public static void main(String[] args) {
        Optional<String> test = Optional.ofNullable("무명소졸");

        if (test.isEmpty()) { //비어 있을 경우 체크 (java 11+) 이전에는 if (!test.isPresent()) 사고의 흐름과 반대되서 가독성이 떨어진다.
            System.out.println(test.get());
        }

        test.ifPresentOrElse(System.out::println, () -> System.out.println("Empty name")); //java 9+

        test.or(() -> Optional.of("Empty name")).ifPresent(System.out::println); //java 9+

        test.orElseThrow(() -> new IllegalArgumentException("Empty name")); //java 10+
    }
}
```