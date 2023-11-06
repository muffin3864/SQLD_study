# 02. SQL 기본 및 활용

## 02.SQL 활용

### 순수 관계 연산자와 SQL 문장 비교

- SELECT 연산은 WHERE 절로 구현

- PROJECT 연산은 SELECT 절로 구현

- (NATURAL) JOIN 연산은 다양한 JOIN 기능으로 구현

- DEVIDE 연산은 현재 사용되지 않음

### ANSI/ISO SQL에서 표시하는 FROM 절의 JOIN 형태

- INNER JOIN

- NATURAL JOIN

- USING 조건절

- ON 조건절

- CROSS JOIN

- OUTER JOIN(LEFT, RIGHT, FULL)

### INNER JOIN

INNER JOIN은 OUTER JOIN과 대비하여 내부 JOIN이라고 하며 JOIN 조건에서 동일한
값이 있는 행만 반환한다.

### CROSS JOIN

테이블 간 JOIN 조건이 없는 경우 생길 수 있는 모든 데이터의 조합을 말한다.
결과는 양쪽 집합의 M*N 건의 데이터 조합이 발생한다.

### LEFT OUTER JOIN

조인 수행시 먼저 표기된 좌측 테이블에 해당하는 데이터를 먼저 읽은 후, 나중 표기된 우측 테이블에서 JOIN 대상 데이터를 읽어온다.
즉, Table A와 B가 있을 때(Table 'A'가 기준이 됨), A와 B를 비교해서 B의 JOIN 칼럼에서 같은 값이 있을 때 그 해당 데이터를 가져오고, B의 JOIN 칼럼에서 같은 값이 없는 경우에는 B 테이블에서 가져오는 칼럼들은 NULL 값으로 채운다.

### FULL OUTER JOIN

조인 수행시 좌측, 우측 테이블의 모든 데이터를 읽어 JOIN하여 결과를 생성한다. 즉, TABLE A와 B가 있을 때(Table 'A', 'B' 모두 기준이 됨), RIGHT OUTER JOIN과 LEFT OUTER JOIN의 결과를 합집합으로 처리한 결과와 동일하다. 

### OUTER JOIN 문장 예시

- LEFT OUTER JOIN

    SELECT X.KEY1,Y.KEY2
    FROM TAB1 X LEFT OUTER JOIN TAB2 Y
    ON (X.KEY1=Y.KEY2)

- RIGHT OUTER JOIN

    SELECT X.KEY1,Y.KEY2
    FROM TAB1 X RIGHT OUTER JOIN TAB2 Y
    ON (X.KEY1=Y.KEY2)

- FULL OUTER JOIN

    SELECT X.KEY1,Y.KEY2
    FROM TAB1 X FULL OUTER JOIN TAB2 Y
    ON (X.KEY1=Y.KEY2)    

