---
tags: String, java, match, matches, regex, 정규표현식, pattern
---
matches()
[https://codechacha.com/ko/java-string-matches/](https://codechacha.com/ko/java-string-matches/)

## ****matches() 기본 예제****

```java
String str = "Welcome to codechacha";

System.out.print("Does String contains regex (.*)code(.*) ? : ");
System.out.println(str.matches("(.*)code(.*)"));

System.out.print("Does String contains regex code ? : ");
System.out.println(str.matches("code"));

System.out.print("Does String contains regex Welcome(.*) ? : " );
System.out.println(str.matches("Welcome(.*)"));
```

위의 예제에서 `(.*)`는 0개 이상으로 이루어진 어떤 문자열을 의미합니다. 그렇기 때문에 정규표현식 `(.*)code(.*)`는 code 양옆에 어떤 문자열이 오든 상관없이 code가 존재하는지만 확인합니다. 이 정규표현식은 `contains("code")`와 거의 동일하다고 생각하면 됩니다.

반면에 정규표현식 `code`는 양 옆에 어떤 문자가 오면 일치하지 않는다고 판단합니다. 그렇기 때문에 false가 리턴됩니다.

`Welcome(.*)`는 Welcome으로 시작하고 그 뒤에 0개 이상의 문자가 오는 패턴이 있을 때 true를 리턴합니다.

## ****True/true 문자열 패턴 찾기****

```java
String str = "True";
System.out.println("Is it true ? : " + str.matches("[Tt]rue"));

str = "true";
System.out.println("Is it true ? : " + str.matches("[Tt]rue"));

str = "yes";
System.out.println("Is it true ? : " + str.matches("[Tt]rue"));

str = "no";
System.out.println("Is it true or yes ? : " + str.matches("[Tt]rue|[Yy]es"));
```

정규표현식 `[Tt]`는 "T" 또는 "t" 둘 중의 하나의 문자를 의미합니다.

## **문자, 숫자 패턴 찾기**

다음 예제는 a가 0개 이상, 그리고 숫자가 0개 이상인 패턴을 찾습니다.

```java
String str = "aaa123";
System.out.println(str.matches("a*[0-9]*"));
```

## **문자열 패턴 찾기**

다음은 "H"로 시작하고 그 다음 어떤 문자가 오고, 마지막으로 "llo"로 끝나고 패턴을 찾습니다.

```java
System.out.println("Hello".matches("H.llo"));
System.out.println("Hallo".matches("H.llo"));
System.out.println("Hollo".matches("H.llo"));
```

## **EX로 시작하는 패턴 찾기**

다음은 "EX_"로 시작하고 그 다음 a~~g의 문자가 오거나 1~~5의 숫자가 오는 패턴을 찾습니다.

```java
System.out.println("Ex_a".matches("Ex_[a-g1-5]"));
System.out.println("Ex_g".matches("Ex_[a-g1-5]"));
System.out.println("Ex_1".matches("Ex_[a-g1-5]"));
System.out.println("Ex_6".matches("Ex_[a-g1-5]"));
```

## **This로 시작하고 .으로 끝나는 패턴**

다음은 This로 시작하고 "."으로 끝나는 패턴을 찾습니다. 만약 "."으로 끝나지 않으면 false를 리턴합니다.

```java
System.out.println("This is the right decision.".matches("This.*\\\\."));
System.out.println("This is me".matches("This.*\\\\."));
System.out.println("This is my mistake.".matches("This.*\\\\."));
```

## **It + a few 패턴 찾기**

It으로 시작하고 a few가 중간에 들어있는 패턴을 찾습니다.

```java
System.out.println("It's been a few days".matches("It.+a few.*"));
System.out.println("It's been a few over a year".matches("It.+a few.*"));
System.out.println("It's been about a week".matches("It.+a few.*"));
```

## **[A-1] 패턴 찾기**

다음은 "[A-숫자]" 로 시작하는 패턴을 찾습니다.

```java
System.out.println("[A-1] Jason".matches("\\\\[A\\\\-.+\\\\].*"));
System.out.println("[A-12] Todd".matches("\\\\[A\\\\-.+\\\\].*"));
System.out.println("[B-12] MJ".matches("\\\\[A\\\\-.+\\\\].*"));
```

## **Pattern으로 matches를 적용하는 방법**

`String.matches()`가 아니라 Pattern 클래스를 이용하여 matches를 적용할 수 있습니다.

다음과 같이 `Pattern.matches()`에 regex와 string을 인자로 전달하면 `String.matches()`와 동일한 결과를 리턴합니다.

```java
String text = "The URL is: <http://mydomain.com>";
String regex = ".*http://.*";

boolean matches = Pattern.matches(regex, text);
System.out.println(matches);
```