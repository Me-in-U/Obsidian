## 1. SQL 쿼리문 결과 예측

SQL 쿼리문 작성 후 예상되는 결과를 예측하기 위해서는
- **테이블의 구조(컬럼, 데이터 타입)**와
- **데이터 분포**
- 그리고 사용된 **조인, 조건, 그룹화 등**의 논리를 잘 이해해야 합니다.

예를 들어, 다음과 같은 쿼리가 있다고 가정해봅니다.
```sql
SELECT department, COUNT(*) AS emp_count, AVG(salary) AS avg_salary
FROM employees
WHERE hire_date >= '2020-01-01'
GROUP BY department
HAVING COUNT(*) > 5
ORDER BY avg_salary DESC;
```
이 쿼리의 결과 예측은 다음과 같습니다.
- **WHERE 절**: 2020년 1월 1일 이후에 입사한 직원만 선택
- **GROUP BY**: 부서별로 그룹화
- **집계 함수**: 각 부서의 직원 수(`COUNT(*)`)와 평균 급여(`AVG(salary)`) 계산
- **HAVING 절**: 그룹 중 직원 수가 5명 초과인 부서만 필터링
- **ORDER BY**: 평균 급여 내림차순 정렬

따라서 결과는 각 부서별로 직원 수와 평균 급여 정보가 표시되며, 5명 이하의 부서는 결과에 포함되지 않고, 평균 급여가 높은 순으로 나열될 것입니다.

---

## 2. SQL 주요 내장 함수

SQL에는 여러 가지 내장 함수가 있어, 날짜 계산, 집계, 문자열 처리 등을 쉽게 할 수 있습니다. 주요 함수들을 몇 가지 분류별로 살펴보겠습니다.

### 2.1 날짜 관련 함수

- **CURDATE() / CURRENT_DATE**
    - 현재 날짜를 반환합니다.
    - 예: `SELECT CURDATE();` → `2025-03-31` (예시)

- **NOW() / CURRENT_TIMESTAMP**
    - 현재 날짜와 시간을 반환합니다.
    - 예: `SELECT NOW();` → `2025-03-31 10:15:30`

- **DATE_ADD(date, INTERVAL expr unit)**
    - 지정한 날짜에 특정 간격을 더합니다.
    - 예: `SELECT DATE_ADD('2025-03-31', INTERVAL 7 DAY);` → `2025-04-07`

- **DATE_SUB(date, INTERVAL expr unit)**
    - 지정한 날짜에서 특정 간격을 뺍니다.
    - 예: `SELECT DATE_SUB('2025-03-31', INTERVAL 1 MONTH);`

- **DATEDIFF(date1, date2)**
    - 두 날짜 간의 차이를 일수로 반환합니다.
    - 예: `SELECT DATEDIFF('2025-04-07', '2025-03-31');` → `7`


### 2.2 집계 함수

- **COUNT(column)**
    - 행의 개수를 세거나, NULL을 제외한 값을 셉니다.
    - 예: `SELECT COUNT(*) FROM employees;`

- **SUM(column)**
    - 지정한 컬럼의 합계를 계산합니다.
    - 예: `SELECT SUM(salary) FROM employees;`

- **AVG(column)**
    - 지정한 컬럼의 평균값을 계산합니다.
    - 예: `SELECT AVG(salary) FROM employees;`

- **MIN(column) / MAX(column)**
    - 지정한 컬럼의 최소값 또는 최대값을 반환합니다.
    - 예: `SELECT MIN(salary), MAX(salary) FROM employees;`


### 2.3 문자열 함수

- **CONCAT(str1, str2, ...)**
    - 여러 문자열을 하나로 연결합니다.
    - 예: `SELECT CONCAT(first_name, ' ', last_name) AS full_name FROM employees;`

- **SUBSTRING(str, start, length)**
    - 문자열의 일부를 추출합니다.
    - 예: `SELECT SUBSTRING('Hello World', 1, 5);` → `Hello`

- **LENGTH(str)**
    - 문자열의 길이를 반환합니다.
    - 예: `SELECT LENGTH('Hello');` → `5`

- CHAR_LENGTH() / CHARACTER_LENGTH()
	- 멀티바이트 문자의 경우 글자 수
	-  CHAR_LENGTH('안녕하세요'); -> 5
- **UPPER(str) / LOWER(str)**
    - 문자열을 모두 대문자 또는 소문자로 변환합니다.
    - 예: `SELECT UPPER('hello');` → `HELLO`

- **TRIM(str)**
    - 문자열의 양쪽 공백을 제거합니다.
    - 예: `SELECT TRIM(' hello ');` → `hello`

- **REPLACE(str, search, replace)**
    - 문자열 내 특정 부분을 다른 문자열로 대체합니다.
    - 예: `SELECT REPLACE('Hello World', 'World', 'SQL');` → `Hello SQL`## 1. SQL 쿼리문 결과 예측
