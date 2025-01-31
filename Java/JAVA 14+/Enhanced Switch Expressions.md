---
tags: java, switch
---
## 1. 개선된 switch문
화살표 case 라벨, 다중 case 라벨, switch 연산식, yield 예약어 등의 기능이 추가되었습니다.
```java
static double getDoubleUsingSwitch(Object o) {
    return switch (o) {
        case Integer i -> i.doubleValue();
        case Float f -> f.doubleValue();
        case String s -> Double.parseDouble(s);
        default -> 0d;
    };
}
```
## 2. 화살표 case 라벨, 다중 case 라벨 (switch1, enhancedSwitch1)
<기존>
```java
switch (day) {
    case MONDAY:
    case FRIDAY:
    case SUNDAY:
        System.out.println(6);
        break;
    case TUESDAY:
        System.out.println(7);
        break;
    case THURSDAY:
    case SATURDAY:
        System.out.println(8);
        break;
    case WEDNESDAY:
        System.out.println(9);
        break;
}
```
<개선>
```java
switch (day) {
    case MONDAY, FRIDAY, SUNDAY	-> System.out.println(6);
    case TUESDAY				-> System.out.println(7);
    case THURSDAY, SATURDAY		-> System.out.println(8);
    case WEDNESDAY				-> System.out.println(9);
}
```
화살표 case 라벨(->)을 사용하면 마지막에 break를 사용한 것과 동일합니다.
주의해야 할 점은 case 라벨(:)을 사용할 때는 실행문이 여러 개여도 중괄호({})로 묶어줄 필요가 없었지만,

화살표 case 라벨(->)을 사용할 때 실행문이 여러 개(즉, 2줄 이상)일 때는 중괄호로 묶어줘야 합니다.

## 3. switch 연산식 (switch2, enhancedSwitch2)
<기존>
```java
int numLetters;
switch (day) {
    case MONDAY:
    case FRIDAY:
    case SUNDAY:
        numLetters = 6;
        break;
    case TUESDAY:
        numLetters = 7;
        break;
    case THURSDAY:
    case SATURDAY:
        numLetters = 8;
        break;
    case WEDNESDAY:
        numLetters = 9;
        break;
    default:
        numLetters = -1;
}
```
<개선>
```java
int numLetters = switch (day) {
    case MONDAY, FRIDAY, SUNDAY	-> 6;
    case TUESDAY				-> 7;
    case THURSDAY, SATURDAY		-> 8;
    case WEDNESDAY				-> 9;
};
```
case TUESDAY -> 7;에서 7을 System.out.println(7)이나 "Seven" 등으로 바꾸면 int type이 아니므로 에러가 발생합니다.

numLetters의 type을 Object로 바꿔주면 "Seven"은 가능하지만,

System.out.println(7)은 return type이 void이므로 여전히 에러가 발생합니다.

즉, switch 연산식을 사용할 때 화살표 case 라벨(->) 뒤에 있는 값이 void type이면 에러가 발생합니다.

## 4. yield 예약어 사용 (enhancedSwitch3, enhancedSwitch4)
yield는 키워드가 아니라 제한된 식별자(restricted identifier)이기 때문에 var처럼 식별자로 사용할 수 있습니다.

방금 전에 본 switch 연산식에서 길이를 return하기 전에 특정 메시지를 출력하고 싶으면 아래와 같이 사용하면 됩니다.
```java
int numLetters = switch (day) {
    case MONDAY, FRIDAY, SUNDAY	-> {
        System.out.print("Six ");
        yield 6;
    }
    case TUESDAY				-> 7;
    case THURSDAY, SATURDAY		-> 8;
    case WEDNESDAY				-> 9;
};
```
향상된 switch 문에서는 중괄호 안에서만 yield 예약어를 사용할 수 있습니다.
따라서 case TUESDAY -> yield 7; 이라고 하면 에러입니다. 
```java
int numLetters = switch (day) {
    case MONDAY, FRIDAY, SUNDAY:
        System.out.print("Six ");
        yield 6;
    case TUESDAY:
        yield 7;
    case THURSDAY, SATURDAY:
        yield 8;
    case WEDNESDAY:
        yield 9;
};
```
yield 예약어는 case 라벨(:)에도 사용 가능합니다.
case 라벨(:)은 실행문이 여러 개일 때 중괄호를 사용하지 않아도 됩니다.

## 5.열거 타입(enum)을 사용하는 이유
```java
enum Day { MONDAY, TUESDAY, WEDNESDAY, THURSDAY, FRIDAY, SATURDAY, SUNDAY }

static int switchError(String s) {
    return switch (s) {
        case "MONDAY", "FRIDAY", "SUNDAY"	-> 6;
        case "TUESDAY"					-> 7;
        case "THURSDAY, SATURDAY"		-> 8;
        case "WEDNESDAY"				-> 9;
        default						-> -1;
    };
}
```
위의 메서드에서 default를 주석 처리하면 "'switch' expression does not cover all possible input values" 에러 메시지를 볼 수 있습니다.

가능한 모든 값에 대하여 일치하는 case 라벨이 하나라도 없으면 위와 같은 에러를 볼 수 있습니다.

위의 예제에서는 String type이므로 가능한 모든 값은 거의 무한대나 마찬가지입니다.

String대신 int type이고, default를 사용하지 않는다면 int 범위의 모든 값에 대하여 case를 사용해야 할 것입니다.

따라서 default를 사용하거나, 필요한 값들로 열거 타입(enum)을 만들어서 사용해야 합니다.