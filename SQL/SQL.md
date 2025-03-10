# Rule

## 용어
- 행(row)
	- 레코드(record)
	- 튜플(tuple)
- 열(column)
	- 속성(attribute)
	- 필드(field)

## DB, TABLE. COLUMN
- 소문자 권장
- snake_case 권장
- 단수형 권장
- 약어사용 x, FULL_NAME 사용
	- pw(X) password(o)
- 테이블의 식별자가되는 컬럼(PK) 컬럼이면 주로 id로 설정

## Single Quotation('), DQ("), BACKTICK(\`) 사용
- 문자열 표현
	- SQ 사용 권장
- alias 줄 때, 별칭 컬럼명에 공백이나 특수문자가 표함됨 경우
	- DQ 사용( AS "테스트_컬럼")
- 객체의 이름을 표현할 때

| 구분     | 백틱(\`)                           | 더블쿼트(" ")                    | 싱글쿼드(' ')                |
| ------ | -------------------------------- | ---------------------------- | ------------------------ |
| 사용 목적  | 테이블명, 컬럼명(식별자)                   | (DBMS에 따라 다름) 식별자 또는 문자열     | 문자열 값 표현                 |
| 예제     | `SELECT `name` FROM `user`;`     | `SELECT "name" FROM "user";` | `SELECT 'John' AS name;` |
| 필요한 경우 | ***예약어, 공백, 특수문자***가 포함된 테이블/컬럼명 | ANSI SQL 표준에서는 식별자에 사용됨      | ***문자 데이터***를 나타낼 때 필요   |

