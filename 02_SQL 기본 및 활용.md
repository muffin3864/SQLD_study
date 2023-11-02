# 02. SQL 기본 및 활용

## 1.SQL 기본

### SQL 문장들의 종류

|명령어의 종류|명령어|설명|
|---|---|---|
|데이터 조작어(DML)|SELECT|데이터베이스에 들어 있는 데이터를 조회하거나 검색 하기 위한 명령어를 말하는것으로 RETRIEVE 라고도 한다.|
|데이터 조작어(DML)|INSERT<br>UPDATE<br>DELETE|데이터베이스의 테이블에 들어 있는 데이터에 변형을 가하는 종류의 명령어들을 말한다. 예를 들어 데이터를 테이블에 새로운 행을 집어넣거나, 원하지 않는 데이터를 삭제하거나 수정하는 것들의 명령어들을 DML이라고 부른다.|
|데이터 정의어(DDL)|CREATE<br>ALTER<br>DROP<br>RENAME|테이블과 같은 데이터 구조를 정의하는데 사용되는 명령어들로 그러한 구조를 생성하거나 변경하거나 삭제하거나 이름을 바꾸는 데이터 구조와 관련된 명령어들을 DDL이라고 부른다.|
|데이터 제어어(DCL)|GRANT<br>REVOKE|데이터베이스에 접근하고 객체들을 사용하도록 권한을 주고 회수하는 명령어를 DCL이라고 부른다.|
|트랜잭션 제어어(TCL)|COMMIT<br>ROLLBACK|논리적인 작업의 단위를 묶어서 DML에 의해 조작된 결과를 작업단위(트랜잭션) 별로 제어하는 명령어를 말한다|

### 테이블 칼럼에 대한 정의 변경

- [Oracle]

    ALTER TABLE 테이블명
    MODIFY (칼럼명1 데이터 유형 [DEFAULT 식] [NOT NULL],
            칼럼명2 데이터 유형 ...);

- [SQL Server]

    ALTER TABLE 테이블명
    ALTER (칼럼명1 데이터 유형 [DEFAULT 식] [NOT NULL],
            칼럼명2 데이터 유형 ...);

### NULL

- 공백이나 숫자 0과는 전혀 다른 값, 조건에 맞는 데이터가 없을 때의 공집합과도 다르다.

- "아직 정의되지 않은 미지의 값"이거나 "현재 데이터를 입력하지 못하는 경우"를 의미한다.

### 제약조건의 종류

- PRIMARY KEY(기본키)

    - 주키로 테이블당 1개만 생성이 가능하다.

    - UNIQUE & NOT NULL 특징을 가짐

- UNIQUE KEY(고유키)

    - 고유키 값은 널값을 가질 수 있다.

- NOT NULL

    - 명시적으로 NULL 입력을 방지한다.

- CHECK

- FOREIGN KEY(외래키)

    - 외래키로 테이블당 여러 개 생성이 가능하다.

    - 외래키 값은 널값을 가질 수 있다.

### 테이블 생성의 주의사항

- 테이블명은 객체를 의미할 수 있는 적절한 이름을 사용한다. 
  가능한 단수형을 권고한다.

- 테이블 명은 다른 테이블의 이름과 중복되지 않아야 한다.

- 한 테이블 내에서는 칼럼명이 중복되게 지정될 수 없다.

- 테이블 이름을 지정하고 각 칼럼들은 괄호 "()" 로 묶어 지정한다.

- 각 칼럼들은 콤마 "."로 구분되고, 테이블 생성문의 끝은 항상 세미콜론 ","으로 끝난다.

- 칼럼에 대해서는 다른 테이블까지 고려하여 데이터베이스 내에서는 일관성 있게 사용하는 것이 좋다
  (데이터 표준화 관점)

- 칼럼 뒤에 데이터 유형은 꼭 지정되어야 한다.

- 테이블명과 칼럼명은 반드시 문자로 시작해야 하고, 벤더별로 길이에 대한 한계가 있다.

- 벤더에서 사전에 정의한 예약어는 쓸 수 없다.

- A-Z, a-z, 0-9, _, $, # 문자만 허용된다.

### 테이블의 불필요한 칼럼 삭제

- ALTER TABLE

    - 테이블 명

- DROP COLUMN

    - 삭제할 칼럼명

### 테이블 이름 변경 (ANSI 표준 기준, 오라클과 동일함)

RENAME OLD_OBJECT_NAME TO NEW_OBJECT_NAME

RENAME STADIUM TO STADIUM_JSC;

### 참조동작

- Delete(/Modify) Action (부서)

    1. Cascade : Master 삭제 시 Child 같이 삭제

    2. Set Null : Master 삭제 시 Child 해당 필드 Null

    3. Set Default : Master 삭제 시 Child 해당 필드 Default 값으로 설정

    4. Restrict : Child 테이블에 PK 값이 없는 경우만 Master 삭제 허용

    5. No Action : 참조무결성을 위반하는 삭제/수정 액션을 취하지 않음

- Insert Action (사원)

    1. Automatic : Master 테이블에 PK가 없는 경우 Master PK를 생성 후 Child 입력

    2. Set Null : Master 테이블에 PK가 없는 경우 Child 외부키를 Null 값으로 분리

    3. Set Default : Master 테이블에 PK가 없는 경우 Child 외부키를 지정된 기본값으로 입력

    4. Dependent : Master 테이블에 PK가 존재할 때만 Child 입력 허용

    5. No Action : 참조무결성을 위반하는 입력 액션을 취하지 않음

### 테이블에 데이터를 입력하는 두가지 유형

- INSERT INTO 테이블명 (COLUMN_LIST) VALUES (COLUMN_LIST에 넣을 VALUE_LIST);

- INSERT INTO 테이블명 VALUES (전체 COLUMN에 넣을 VALUE_LIST)

### 테이블에 입력된 데이터 조회

SELECT
    [ALL/DISTINCT]
    보고 싶은 칼럼명,
    보고 싶은 칼럼명, ...
FROM 해당 칼럼들이 있는 테이블 명;

- ALL : Default 옵션이므로 별도로 표시하지 않아도 된다.
        중복된 데이터가 있어도 모두 출력한다.

- DISTINCT : 중복된 데이터가 있는 경우 1건으로 처리해서 출력한다.

### DROP, TRUNCATE, DELETE

|DROP|TRUNCATE|DELETE|
|:---:|:---:|:---:|
|DDL|DDL<br>(일부 DML 성격 가짐)|DML|
|Rollback 불가능|Rollback 불가능|Commit 이전 Rollback 가능|
|Auto Commit|Auto Commit|사용자 Commit|
|테이블이 사용했던 Storage를 모드 Realease|테이블이 사용했던 Storage중 최초 테이블 생성시 할당된 Storage만 남기고 Release|데이터를 모두 Delete해도 사용했던 Storage는 Release되지 않음|
|테이블의 정의 자체를 완전히 삭제함|테이블을 최초 생성된 초기상태로 만듬|데이터만 삭제|

### 데이터베이스 트랜잭션의 4가지 특성
|특성|설명|
|:---:|---|
|원자성<br>(Atomicity)|트랜잭션에서 정의된 연산들은 모두 성공적으로 실행되던지 아니면 전혀 실행되지 않은 상태로 남아 있어야 한다.<br>(All or Nothing)|
|일관성<br>(consistency)|트랜잭션이 실행 되기 전의 데이터베이스 내용이 잘못 되어 있지 않다면 트랜잭션이 실행된 이후에도 데이터베이스의 내용에 잘못이 있으면 않된다.|
|고립성<br>(isolation)|트랜잭션이 실행되는 도중에 다른 트랜잭션의 영향을 받아 잘못된 결과를 만들어서는 안된다.|
|지속성<br>(durability)|트랜잭션이 성공적으로 수행되면 그 트랜잭션이 갱신한 데이터베이스의 내용은 영구적으로 저장된다.|

### 롤백(Rollback)

데이터 변경 사항이 취소되어 데이터의 이전 상태로 복구되며, 관련된 행에 대한 잠금(LOCKING)이 풀리고
다른 사용자들이 데이터 변경을 할 수 있게 된다.

### BEGIN TRANSACTION

BEGIN TRANSACTION으로 시작하고 COMMIT 또는 ROLLBACK으로 트랜잭션을 종료한다.
ROLLBACK 구문을 만나면 최초의 BEGIN TRANSACTION 시점까지 모두 ROLLBACK이 수행된다.

저장점(SAVEPOINT)을 정의하면 롤백 할 때 트랜잭션에 포함된 전체 작업을 롤백하는것이 아니라
현 시점에서 SAVEPOINT까지 트랜잭션의 일부만 롤백할 수 있다.

### WHERE절

WHERE절은 FROM 절 다음에 위치한다.

- 조건식

    - 칼럼 명(보통 조건식의 좌측에 위치)

    - 비교 연산자

    - 문자, 숫자, 표현식 (보통 조건식의 우측에 위치)

    - 비교 칼럼명 (JOIN 사용시)

### 연산자의 우선순위

1. 괄호로 묶은 연산

2. 부정 연산자(NOT)

3. 비교 연산자(=, >, >=, <, <=)와 SQL 비교 연산자(BETWEEN a AND b, IN (list), LIKE, IS NULL)

4. 논리 연산자 중 AND, OR의 순으로 처리

### NULL의 연산

- NULL 값과의 연산은 NULL 값을 리턴

- NULL 값과의 비교연산은 거짓(FALSE)을 리턴

- 특정 값보다 크다, 적다라고 표현할 수 없음

### 연산자의 종류
- 비교 연산자

    - = : 같다.

    - '>' : 보다 크다.

    - '>=' : 보다 크거나 같다.

    - < : 보다 작다.

    - <= : 보다 작거나 같다.

- SQL 연산자

    - BETWEEN a AND b : a와 b 값 아시에 있으면 된다.(a와 b 값이 포함됨)

    - IN (list) : 리스트에 있는 값 중에서 어느 하나라도 일치하면 된다.

    - LIKE '비교문자열' : 비교문자열과 형태가 일치하면 된다.(%, _ 사용)

    - IS NULL : NULL 값인 경우

- 논리 연산자

    - AND : 앞에 있는 조건과 뒤에 오는 조건이 참(TRUE)이 되면 결과도 참(TRUE)이 된다.
            즉, 앞의 조건과 뒤의 조건을 동시에 만족해야 한다.

    - OR : 앞의 조건이 참(TRUE)이거나 뒤의 조건이 참(TRUE)이 되어야 결과도 참(TRUE)이 된다.
            즉, 앞뒤의 조건 중 하나만 참(TRUE)이면 된다.

    - NOT : 뒤에 오는 조건에 반대되는 결과를 되돌려 준다.

- 부정 비교 연산자

    - != : 같지 않다.

    - ^= : 같지 않다.

    - <> : 같지 않다.(ISO표준, 모든 운영체제에서 사용 가능)

    - NOT 칼럼명 = : ~와 같지 않다.

    - NOT 칼럼명 > : ~보다 크지 않다.

- 부정 SQL 연산자

    - NOT BETWEEN a AND b : a와 b의 값 사이에 있지 않다. (a, b 값을 포함하지 않는다.)

    - NOT IN (list) : list 값과 일치하지 않는다.

    - IS NOT NULL : NULL 값을 갖지 않는다.

# 함수의 종류

- 함수

    - 내장함수 : 벤더에서 제공하는 함수

        - 단일행 함수

        - 다중행 함수

            - 집계 함수

            - 그룹 함수

            - 윈도우 함수

    - 사용자가 정의할 수 있는 함수

### 단일행 문자형 함수의 종류

|문자형 함수|함수 설명|
|---|---|
|LOWER(문자열)|문자열의 알파벳 문자를 소문자로 바꾸어 준다.|
|UPPER(문자열)|문자열의 알파벳 문자를 대문자로 바꾸어 준다.|
|ASCII(문자)|문자나 숫자를 ASCII 코드 번호로 바꾸어 준다.|
|CHR/CHAR(ASCII번호)|ASCII 코드 번호를 문자나 숫자로 바꾸어 준다.|
|CONCAT(문자열1, 문자열2)|Oracle, My SQL에서 유효한 함수이며 문자열1과 문자열2를 연결한다. 합성 연산자'||'(Oracle)나 '+'(SQL Server)와 동일하다.|
|SUBSTR/SUBSTRING(문자열, m[, n])|문자열 중 m위치에서 n개의 문자 길이에 해당하는 문자를 돌려준다. n이 생략되면 마지막 문자까지이다.|
|LENGTH/LEN(문자열)|문자열의 개수를 숫자값으로 돌려준다.|
|LTRIM(문자열 [, 지정문자])|문자열의 첫 문자부터 확인해서 지정 문자가 나타나면 해당 문자를 제거한다.(지정 문자가 생략되면 공백 값이 디폴트) SQL Server에서는 LTRIM 함수에 지정문자를 사용할 수 없다. 즉, 공백만 제거할 수 있다.|
|RTIM(문자열, [, 지정문자])|문자열의 마지막 문자부터 확인해서 지정 문자가 나타나는 동안 해당 문자를 제거한다.(지정 문자가 생략되면 공백 값이 디폴트)<br>SQL Server에서는 LTRIM함수에 지정문자를 사용할 수 없다. 즉, 공백만 제거할 수 있다.|
|TRIM([leading/trailing/both] 지정문자 FROM 문자열)|문자열에서 머리말, 꼬리말, 또는 양쪽에 있는 지정 문자를 제거한다.<br>(leading / trailing / both 가 생략되면 both가 디폴트)<br>SQL Server에서는 TRIM 함수에 지정문자를 사용할 수 없다. 즉, 공백만 제거할 수 있다.|

※ 주: Oracle함수/SQL Server함수 표시, '/'없는 것은 공통 함수

### Dual 테이블의 특성

- 사용자 SYS가 소유하며 모든 사용자가 액세스 가능한 테이블이다.

- SELECT ~ FROM ~ 의 형식을 갖추기 위한 일종의 DUMMY 테이블이다.

- DUMMY라는 문자열 유형의 칼럼에 X라는 값이 들어 있는 행을 1건 포함하고 있다.

### 단일행 함수의 종류

|종류|내용|함수의 예|
|:---:|---|---|
|문자형 함수|문자를 입력하면 문자나 숫자 값을 반환한다.|LOWER, UPPER, SUBSRT/SUBSRTING, LENGTH/ LEN, LTRIM, RTRIM, TRIM, ASCII,|
|숫자형 함수|숫자를 입력하면 숫자 값을 반환한다.|ABS, MOD, ROUND, TRUNC, SIGN, CHR/CHAR, CEIL/CEILING, FLOOR, EXP, LOG, LN, POWER, SIN, COS, TAN|
|날짜형 함수|DATE 타입의 값을 연산한다.|SYSDATE/GETDATE, EXTRACT/DATEPART, TO_NUMBER(TO_CHAR(d, 'YYYY'/'MM'/'DD'))/YEAR/MONTH/DAY|
|변환형 함수|문자, 숫자, 날짜형 값의 데이터 타입을 변환한다.|TO_NUMBER, TO_CHAR, TO_DATE/ CAST, CONVERT|
|NULL 관련 함수|NULL을 처리하기 위한 함수|NVL/ISNULL, NULLIF, COALESCE|



## 2. SQL 활용

## 3. SQL 최적화 기본 원리
