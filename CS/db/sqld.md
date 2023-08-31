<h1>1. sqld 문제집 풀면서 알게된것</h1>
<hr>

* 파생속성 : 다른 속성 영향 , 계산된 값.

* 쿼리 문제 나오면 내가 따라 짜보기

* DCL => grant, revoke / TCL => commit , rollback

* 테이블명 , 컬럼명 문자로 시작

* RENAME ~ TO 으로 테이블 이름 변경을 할 수 있다

* VARCHAR("1") 문자수를 잘 봐야되는데 체크 안해서 틀린 문제가 있다.

* NULL 이면 표기 안해도 기본값이 NULL 이다.

* Insert into values ( ???) 이 문구를 벗어나면 Insert 문 벗어나는거 체크하면 된다.

* 오류나는걸 찾는건지 아닌지 체크 잘하자.

* 중복 DISTINCT 이다.

* 사용 용도가 없다 그러면 DELETE FROM 그냥 하면된다 (* 안씀)

* 원자성 => 트랜잭션에서 정의된 연산들은 모두 성공적으로 실행되던지 아니면 전혀 실행되지 않은 상태로 남아 있어야 한다.

* 일관성 => 트랜잭션이 실행 되기 전의 데이터베이스 내용이 잘못 되어 있지 않다면 트랜잭션이 실행된 이후에도 데이터베이스의 내용에 잘못이 있으면 안된다.

* 고립성 => 트랜잭션이 실행되는 도중에 다른 트랜잭션의 영향을 받아 잘못된 결과를 만들어서는 안된다.

* 지속성 => 트랜잭션이 성공적으로 수행되면 그 트랜잭션이 갱신한 데이터베이스의 내용은 영구적으로 저장된다.

* Dirty Read => 다른 트랜잭션에 의해 수정되었지만 아직 커밋되지 않은 데이터를 읽는 것을 말한다.


# 과목 II

### ORDER BY 문장
* where
* group by
* having
* order by

* ASC 오름차순
* DESC 내림차순

### 55번 문제

~~~sql
ORDER BY (CASE WHEN ID = 999 THEN 0 ELSE ID END

~~~
* order by 절 case문에 의해 999는 0으로 치환되고 그외는 ID 값으로 정렬된다.

### 56번 문제

~~~sql
SELECT 지역, 매출금액 FROM 지역별매출 ORDER BY 년 ASC;
~~~
* SELECT 절의 실행순서에 의해서 SELECT 다음 ORDER BY절이 수행되기 때문에 SELECT 절에 기술되지 않는 "년"칼럼으로 정렬하는 것은 논리적으로 틀렸다. 하지만 오라클은 행기반이기에 데이터를 액세스할 때 행 전체 칼럼을 메모리에 로드되서 가능하다.

* 단, 아래와 같은 SQL일 겨웅에는 정렬할 수 없다.
~~~sql
SELECT 지역, 매출금액
FROM (
    SELECT 지역, 매출금액
      FROM 지역별매출
   )
ORDER BY 년 ASC;
~~~

* IN-LINE VIEW가 먼저 수행되어서 더 이상 SELECT절 외 칼럼을 사용할 수 없기 때문.

### 57번 문제

* ORDER BY 절에 컬럼명 대신 Alias 명이나 컬럼 순서를 나타내는 정수를 혼용하여 사용할 수 있다.

### ORDER BY 절 특징
* 기본 정렬순서 : 오름차순
* 숫자형 => 가장 작은 값부터
* 날짜형 => 가장 빠른 날부터

* Oracle : NULL 값을 가장 큰값

* SQL Server : NULL 값으 가장 작은 값

### 58번 문제

```sql
SELECT ID, AMT
FROM TBL
ORDER BY (CASE WHEN ID = 'A' THEN 1 ELSE 2 END),
          AMT DESC
```
* CASE절을 이용해서 원래의 정렬 순서를 변경하였다. 그래서 ID가 'A'인 것이 가장 먼저 표시되도록 하였다.

### Select 문장 실행 순서
* FROM => WHERE => Group by => Having => Select => Order By

### TOP () 예제 사원
* 테이블에서 급여가 높은 2명을 내림차순으로 출력하는데 같은 급여를 받는 사원이 있으면 같이 출력한다.

```sql
SELECT TOP(2) WITH TIES ENAME, SAL
FROM EMP
ORDER BY SAL DESC;
```

### EQUI JOIN 문장
* WHERE 절에 JOIN 조건을 넣는다.

### ANSI/ISO SQL 표준 EQUI JOIN 문장
* ON 절에 JOIN 조건을 넣는다.

### 62번 문제

```sql
SELECT 영화.영화명, 배우.배우명, 출연료
FROM 배우, 영화, 출연
WHERE 출연료 >= 8888
AND 출연.영화번호 = 영화.영화번호
AND 출연.배우번호 = 배우.배우번호;
```
* 영화명과 배우명은 출연 테이블이 아니라 영화와 배우 테이블에서 가지고 와야 하는 속성이므로 출연테이블의 영화번호와 영화테이블의 영화번호 및 출연테이블의 배우번호와 배우테이블의 배우번호를 조인하는 SQL문을 작성해야 함.

### 63번 문제 (어렵다..)





