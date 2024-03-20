---
tags: java, regex, 정규표현식
---
[https://codechacha.com/ko/java-regex/](https://codechacha.com/ko/java-regex/)

정규표현식(Regular expressions)은 줄여서 Regex라고 합니다. Regex는 문자열에 어떤 패턴의 문자들이 있는지 찾는데 도움을 줍니다.

이 글은 Regex의 패턴과 사용방법 위주로 정리하였습니다. Regex는 대부분 알고 있지만, 적용할 표현들이 헷갈렸다면 이 글을 참고하시면서 패턴을 작성해보세요.

## **Metacharacters**

`Metacharacters`는 Regex의 패턴에서 어떤 문자가 특별한 의미를 갖는 것을 말합니다. 예를 들어, `\\d`는 0에서 9사이의 숫자를 의미합니다.

자주 사용되는 Metacharacters를 정리하였습니다.

|Regular Expression|Description|
|---|---|
|.|어떤 문자 1개를 의미 line break 제|
|^regex|^ 다음 regex로 line을 시작하는지|
|regex$|$ 앞의 regex가 line의 마지막으로 끝나는지|
|[abc]|a, b, c 중의 문자 1개|
|[abc][vz]|a, b, c 중에 문자 1개와 v, z 중에 문자 1개의 조합|
|[^abc]|a, b, c를 제외한 문자 1개|
|[a-d1-7]|ad, 17 사이의 문자 1개|
|X|Z|
|\d|0~9 사이의 숫자, [0-9]와 동일|
|\D|숫자가 아닌 어떤 문자, [^0-9]와 동일|
|\s|whitespace 1개, [\t\n\x0b\r\f]와 동일|
|\S|whitespace를 제외한 문자|
|\S+|whitespace를 제외한 여러 문자|
|\w|Alphanumeric(alphabet, 숫자) 문자, [a-zA-Z_0-9]와 동일|
|\W|Alphanumeric을 제외한 문자(whitespace 등)|
|\b|단어의 경계(공백)를 찾습니다|

### **예제**

- 패턴에서 `"."`는 문자 1개에 해당합니다. 그 문자가 숫자인지 whitespace인지는 중요하지 않습니다. 아래 예제에서 패턴 `"ab."`는 "ab"와 일치하지 않습니다. "ab" 뒤에 문자가 없기 때문입니다.
- `\\s`는 whitespace 1개, `\\S`는 whitespace를 제외한 문자 1개를 의미합니다. 자바에서 `\\`를 표현하려면 `\\\\`처럼 사용해야 합니다.

```java
@Test
public void ex1() {
    String pattern = "ab.";
    assertFalse("ab".matches(pattern));
    assertTrue("abc".matches(pattern));

    pattern = "ab\\\\s\\\\S";
    assertFalse("ab  ".matches(pattern));
    assertTrue("ab c".matches(pattern));
}
```

> 예제는 Junit을 이용하여 작성되었습니다. assertTrue()는 결과로 true가 리턴된다는 것을 의미하며 assertFalse()는 결과로 false가 리턴된다는 것을 의미합니다.

- `^`는 문자열의 _**시작지점**_을 찾습니다. 따라서 `^` 다음으로 오는 패턴으로 문자열이 시작되는 것을 찾습니다. 아래 예제에서 `replaceAll(regex, replacement)`은 regex와 일치하는 내용을 replacement로 교체합니다. 결과에서 `*`로 변경된 내용이 regex와 일치하는 것이라고 생각하시면 됩니다.

```java
@Test
public void ex2() {
  String result;
  result = "The cat sat on the mat.".replaceAll("[Tt]he", "*");
  System.out.println(result);

  result = "The cat sat on the mat.".replaceAll("^[Tt]he", "*");
  System.out.println(result);
}
```

결과

`* cat sat on * mat.

- cat sat on the mat.`

- `$`는 문자열의 _**종료지점**_을 찾습니다. 따라서 `$` 앞의 패턴으로 문자열이 끝나는 것을 찾습니다.

```java
@Test
public void ex3() {
    String result;
    result = "The cat sat on the mat. and the cat".replaceAll("cat", "*");
    System.out.println(result);

    result = "The cat sat on the mat. and the cat".replaceAll("cat$", "*");
    System.out.println(result);
}
```

결과

`The * sat on the mat. and the * The cat sat on the mat. and the *`

- `\\b`는 단어의 경계선을 찾는 역할을 합니다. 다음 예제를 보시면 경계선의 의미가 무엇인지 이해할 수 있습니다. 단어 양 옆에 `\\b`를 사용하여 다른 문자와 결합되지 않은, 독립적인 단어를 찾을 수 있습니다.

```java
@Test
public void ex15() {
    String result;
    result = "This island is beautiful.".replaceAll("is", "*");
    System.out.println(result);

    result = "This island is beautiful.".replaceAll("\\\\bis\\\\b", "*");
    System.out.println(result);
}
```

결과

`Th* *land * beautiful. This island * beautiful.`

- `[ ]`는 내부의 문자열과 일치하는 문자 1개를 찾습니다. `"-"`를 사용하여 범위를 지정할 수도 있습니다.

```java
@Test
public void ex4() {
    String pattern = "[abc][vz]";
    assertTrue("av".matches(pattern));
    assertFalse("ac".matches(pattern));

    pattern = "Ex_[a-g1-5]";
    assertTrue("Ex_g".matches(pattern));
    assertFalse("Ex_6".matches(pattern));
}
```

- 다음은 숫자, 문자, 공백을 표현하는 Metacharacters들에 대한 예제입니다. 참고로, 자바는 `\\`를 표현하려면 `\\\\`로 입력해야 합니다. 가독성이 떨어지는 면이 있습니다.

```java
@Test
public void ex5() {
    String pattern = "\\\\d\\\\D";
    assertTrue("1a".matches(pattern));
    assertFalse("a1".matches(pattern));

    pattern = "\\\\d\\\\s\\\\D";
    assertTrue("1 a".matches(pattern));

    pattern = "\\\\d\\\\s\\\\S\\\\D";
    assertTrue("1 1a".matches(pattern));

    pattern = "\\\\w\\\\W";
    assertTrue("1 ".matches(pattern));
}
```

## **Quantifiers**

Quantifiers는 요소들을 얼마나 반복시킬지 정의합니다.

| Regular Expression | Description                                                                                         |
| ------------------ | --------------------------------------------------------------------------------------------------- |
| *                  | 0회 이상 반복                                                                                       |
| +                  | 1회 이상 반복                                                                                       |
| ?                  | 0 또는 1회만                                                                                        |
| i                  | 찾는 문자가 영문일 경우 대소문자를 구별하지 않음                                                    |
| g                  | g가 없으면 데이터의 왼쪽부터 규칙에 일치하는 문자 한 개만 찾음, 있으면 규칙에 맞는 모든 문자를 찾음 |
| m                  | 데이터의 행이 바뀌어도 규칙에 맞는 문자를 찾음                                                      |
| ^                  | 문자열 앞에서부터 규칙에 일치하는 문자를 찾음                                                       |
| $                  | 문자열 끝 부분 규칙에 맞는 문자를 찾음                                                              |
| {X}                | X회 이상 반복                                                                                       |
| {X,Y}              | X~Y 사이의 수만큼 반복                                                                              |
| *?                 | 가장 적게 일치하는 패턴을 찾음                                                                      |
### **예제**

- `은`  앞의 요소가 0이상 반복되는 것을 의미합니다.
- `+`는 1이상 반복되는 것을 의미합니다. 이것은 요소가 1개도 없으면 패턴과 일치하지 않는다는 의미입니다.

```java
@Test
public void ex6() {
    String pattern = "a*[0-9]*";
    assertTrue("aaa123".matches(pattern));
    assertTrue("aaa".matches(pattern));

    pattern = "a*[0-9]+";
    assertTrue("aaa123".matches(pattern));
    assertFalse("aaa".matches(pattern));
}
```

- `?`는 요소가 0 또는 1회만 반복되는 것을 의미합니다.
- `{X,Y}`는 X~Y 사이의 수만큼 반복된다는 것을 의미하며, 위에서 문자열 1개로 처리했던 것을 모두 표현할 수 있습니다. 아래 예제에서 `{0,1}`은 `?`와 동일한 의미입니다.

```java
@Test
public void ex7() {
    String pattern = "a*[0-9]?";
    assertTrue("aaa".matches(pattern));
    assertFalse("aaa12".matches(pattern));

    pattern = "a*[0-9]{0,1}";
    assertTrue("aaa".matches(pattern));
    assertFalse("aaa12".matches(pattern));
}
```

## **Grouping**

패턴에 그룹을 지정할 수 있습니다. 그룹은 `()`로 지정하며, 그룹을 표현할 때는 `$1`처럼 `$`다음에 그룹의 번호를 입력합니다. 패턴에서 가장 왼쪽 그룹이 1번으로 시작합니다.

다음은 Grouping에 대한 예제입니다. 예제의 패턴은 `"1 character + whitespaces + 1 character"`을 의미합니다. 그룹은 3개로 나누었습니다.

`replaceAll(pattern, replacement)`는 pattern과 일치하는 문자열을 replacement로 변환합니다.

아래 예제에서 패턴과 일치하는 것은 `"o w"`이며, 첫번째 예제는 일치하는 문자열을 `"-"`로 변환하였습니다.

두번째는 replacement에는 `"$1-$3"`을 입력하였는데, 이것은 Format과 유사합니다. 그룹1과 그룹3에 해당하는 내용으로 변환이 됩니다.
### 예제

```java
@Test
public void ex8() {
    String pattern = "(\\\\w)(\\\\s+)([\\\\w])";
    System.out.println("Hello     World".replaceAll(pattern, "-"));

    pattern = "(\\\\w)(\\\\s+)([\\\\w])";
    System.out.println("Hello     World".replaceAll(pattern, "$1-$3"));
}
```

결과

`Hell-orld Hello-World`

## **Regex를 지원하는 String 메소드**

String 클래스는 Regex를 지원하는 메소드들이 있습니다.

|Method|Description|
|---|---|
|String.matches(regex)|String이 regex와 일치하면 true 리턴|
|String.split(regex)|regex와 일치하는 것을 기준으로 String을 분리하여 배열로 리턴|
|String.replaceFirst(regex, replacement)|regex와 가장 먼저 일치하는 것을 replacement로 변환|
|String.replaceAll(regex, replacement)|regex와 일치하는 모든 것을 replacement로 변환|

### 예제

```java
@Test
public void ex9() {
    String pattern = "a*[0-9]*";
    assertTrue("aaa123".matches(pattern));

    pattern = "\\\\s";
    String arr[] = "Hello World Java Regex".split(pattern);
    System.out.println(Arrays.asList(arr));

    pattern = "Hello";
    System.out.println("Hello World Hello World ".replaceFirst(pattern, "Regex"));

    pattern = "Hello";
    System.out.println("Hello World Hello World ".replaceAll(pattern, "Regex"));
}
```

결과

`[Hello, World, Java, Regex] Regex World Hello World Regex World Regex World`

## **Pattern**

Regex는 "\d"와 같이 String으로 표현할 수 있습니다. `Pattern`은 컴파일된 Regex라고 표현합니다.

다음과 같이 Regex String을 컴파일하여 Pattern이라는 객체로 만듭니다.

```java
Pattern pattern = Pattern.compile("\\\\bcat\\\\b");
```

## **Matcher**

`Matcher`는 match operation을 수행하는 engine입니다. Matcher는 다음과 같이 Pattern 객체로부터 생성됩니다. 인자로 패턴을 찾을 문자열을 전달합니다.

`Pattern pattern = Pattern.compile("\\\\bcat\\\\b"); Matcher matcher = pattern.matcher("cat cat cat cattie cat");`

Matcher를 통해서 찾은 패턴은 다음과 같이 결과를 출력할 수 있습니다. `start()`는 첫번째 문자의 index, `end()`는 마지막 문자의 index를 리턴합니다. `group()`은 일치하는 문자열을 리턴합니다.
### 예제

```java
@Test
public void ex10() {
    Pattern pattern = Pattern.compile("\\\\bcat\\\\b");
    Matcher matcher = pattern.matcher("cat cat cat cattie cat");
    int count = 0;
    while(matcher.find()) {
        count++;
        System.out.println("Match number " + count);
        System.out.println("group(): " + matcher.group());
        System.out.println("start(): " + matcher.start());
        System.out.println("end(): " + matcher.end());
    }
}
```

결과

`Match number 1 group(): cat start(): 0 end(): 3 Match number 2 group(): cat start(): 4 end(): 7 Match number 3 group(): cat start(): 8 end(): 11 Match number 4 group(): cat start(): 19 end(): 22`

## **다양한 예제**

Regex를 사용한 다양한 예제를 소개합니다.

### **숫자 패턴 찾기**

```java
@Test
public void ex11() {
    Pattern pattern = Pattern.compile("\\\\d{3}-\\\\d{5}");
    Matcher matcher = pattern.matcher("123-45678");
    assertTrue(matcher.find());
}
```

### **Backreferences**

Regex에서 이전에 사용된 subpattern을 참조하는 것도 가능합니다. 이것을 Backreferences라고 합니다.

Backreferences는 `\\n`으로 표현합니다. 예를 들어, `\\1`는 첫번째 subpattern이며, `\\2`는 두번째 subpattern입니다.

아래 예제에서 `\\1`은 첫번째 subpattern `(..)`을 의미합니다.

```java
@Test
public void ex12() {
    Pattern pattern = Pattern.compile("c(..) s\\\\1");
    Matcher matcher = pattern.matcher("The cat sat on the mat");
    assertTrue(matcher.find());
}
```

### **중복된 단어 패턴 찾기**

아래 예제의 Regex에서 `\\1`은 첫번째 subpattern `("\\w+")`을 의미합니다. 따라서 동일한 단어가 연달아 오는 String은 이 패턴과 일치하게 됩니다.

```java
@Test
public void ex12_2() {
    Pattern pattern = Pattern.compile("\\\\b(\\\\w+)\\\\s+\\\\1\\\\b");
    Matcher matcher = pattern.matcher("hello world world");
    assertTrue(matcher.find());
}
```

### **Replace**

Replace와 관련된 예제입니다.

```java
@Test
public void ex13() {
    String result;
    Pattern p = Pattern.compile("dog");
    Matcher m = p.matcher("The dog says meow. All dogs say meow.");
    System.out.println(m.replaceAll("cat"));

    result = "The cat sat on the mat.".replaceAll("at[.]", "*");
    System.out.println(result);

    result = "The cat sat on the mat.".replaceAll("at[.]?", "*");
    System.out.println(result);

    result = "The cat sat on the mat.".replaceAll("[a-z]+", "*");
    System.out.println(result);
}
```

결과

`The cat says meow. All cats say meow. The cat sat on the m* The c* s* on the m* T* * * * * *.`

### *_+? 또는 _? 의 예제__

`?`가 단독으로 사용되면 0 또는 1회라는 의미입니다. 하지만 `+`, `*` 등과 함께 사용되면 가장 적은 조건으로 매칭되는 문자열을 찾는다는 의미입니다.

아래 예제에서 `+`만 사용했을 때와 `+?`를 사용했을 때의 결과를 비교하면 이해가 쉽습니다.

첫번째 예제는 가장 크게 일치하는 `cat~mat`의 문자열을 패턴으로 인식하였습니다.

두번째 예제는 가장 적게 일치하는 `cat`를 문자열의 패턴으로 인식하였습니다.

```java
@Test
public void ex14() {
    String result;
    result = "The cat sat on the mat.".replaceAll("c.+t", "*");
    System.out.println(result);

    result = "The cat sat on the mat.".replaceAll("c.+?t", "*");
    System.out.println(result);
}
```

결과

`The *. The * sat on the mat.`