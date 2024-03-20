---
tags: java, sort, comparable, comparator, 오름차순, 내림차순
---
- Comparator: 기본 정렬기준 외에 다른 기준으로 정렬하고자 할 때 사용
- Comparable: 기본 정렬기준을 구현하는데 사용

## 비교
- **구현 위치**:
    - `Comparable`: 정렬할 클래스 내부에 구현
    - `Comparator`: 별도의 클래스에 구현
- **유연성**:
    - `Comparable`: 한 가지 정렬 기준만 정의할 수 있습니다.
    - `Comparator`: 여러 가지 정렬 기준을 정의할 수 있습니다.
- **메서드**:
    - `Comparable`: `compareTo(T o)`
    - `Comparator`: `compare(T o1, T o2)`
- **사용 시나리오**:
    - `Comparable`: 객체의 자연적인 순서를 정의할 때 사용
    - `Comparator`: 다양한 정렬 기준을 적용할 때 사용

## 순서
### 오름차순
- 한글순 > 소문자 > 대문자 > 숫자

### 내림차순
- 숫자 > 대문자 > 소문자 > 한글순

## 반환
compare()와 compareTo()는 두 객체의 비교결과를 반환하도록 작성
- a > b : 양수를 반환
- a == b : 0을 반환
- a < b : 음수를 반환

return o1 - o2; (같으면 0, 음수면 -1, 양수면 +1) 음수일 경우 : 두 원소의 위치를 교환 안함 양수일 경우 : 두 원소의 위치를 교환 함