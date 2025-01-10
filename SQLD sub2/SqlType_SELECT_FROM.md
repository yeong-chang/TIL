## SQL의 종류


| 종류  | 명령어                         |
|-----|----------------------------------|
| DDL | `CREATE`, `ALTER`, `DROP`, `TRUNCATE` |
| DML | `SELECT`, `INSERT`, `UPDATE`, `DELETE` |
| DCL | `GRANT`, `REVOKE`               |
| TCL | `COMMIT`, `ROLLBACK`, `SAVEPOINT`, `SET TRANSACTION` |
| DQL | `SELECT`                        |


### SELECT 절

#### 실행 순서
- FROM → WHERE → GROUP BY → HAVING →SELECT → ORDER BY

1. FROM 절: 데이터를 가져옴.
2. WHERE 절: 조건에 맞는 행을 필터링.
3. SELECT 절: 선택된 행에서 컬럼을 추출하고, 이때 별칭이 정의됨.
4. GROUP BY 절: 지정한 컬럼(혹은 표현식)을 기준으로 그룹화.
5. HAVING 절: 그룹화된 결과에 대한 조건을 필터링.
6. ORDER BY 절: 최종 결과를 정렬.

#### AS

- 별칭 생성(ALIAS)

```sql
SELECT ENAME AS 사원이름 FROM EMP;
-- ENAME이 사원이름이라는 별칭으로 출력된다.
```

쌍따옴표 전달이 필요한 경우

1. 별칭에 공백을 포함하는 경우
2. 별칭에 특수문자를 포함하는 경우(”_” 제외)
3. 별칭 그대로 전달한 경우(대소문자를 그대로 출력하고자 할 떄)
```sql
select SAL AS "급 여"
from EMP e1,
DEPT d1
where e1.DEPTNO = d1.DEPTNO;
```
실행시     
![sqld별칭.png](sqldimg2%2Fsqld%EB%B3%84%EC%B9%AD.png)   

#### ALIAS 사용시 주의사항

- ORDER BY 절은 SELECT문보다 늦게 실행되기 때문에 ORDET BY 절 에서만 별칭을 사용 가능하다.


#### SELECT문 요약

- SELECT문은 출력할 컬럼명, 연산결과 등을 작성하는 문장임 컬럼명에 별칭을 주기도 한다.

### FROM 절

- 데이터를 불러올 테이블명 또는 뷰명을 전달
- 데이터를 불러오는 테이블이 여러개 라면 , 로 구분 -> 만약 join 조건이 없이 테이블을 불러올시 카타시안 곱이 발생 한다.
- ORACLE에서는 FROM절을 생략 할 수 없다.   

![sqld_FROM절 생략시.png](sqldimg2%2Fsqld_FROM%EC%A0%88%20%EC%83%9D%EB%9E%B5%EC%8B%9C.png)

만약 테이블명이 의미상 필요 없는 경우에는 dual테이블을 사용한다.  
![dual테이블 사용.png](sqldimg2%2Fdual%ED%85%8C%EC%9D%B4%EB%B8%94%20%EC%82%AC%EC%9A%A9.png)

```sql
select SAL AS "급 여"
from EMP e1,
DEPT d1
where e1.DEPTNO = d1.DEPTNO; //여기 where조건이 join 조건임
```