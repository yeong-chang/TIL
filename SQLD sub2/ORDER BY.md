## ORDER BY 절

- 데이터가 출력되는 행의 순서를 사용자가 변경하고자 할 때 ORDER BY절을 사용
- 정렬순서를 오름차순(ASC), 내림차순(DESC)으로 전달 (생략 시 오름차순 정렬)
- 유일하게 SELECT절에 정의한 컬럼 별칭 사용 가능

### ORDER BY를 사용했지만 동일한 결과가 있을때  
![ORDER BY 조건 2개.png](sqldimg2%2FORDER%20BY%20%EC%A1%B0%EA%B1%B4%202%EA%B0%9C.png)  
이런식으로 조건을 여러개 사용했을때 HIREDATE가 1981-12-03 으로 같은값이 두개지만
ENPNO를 DESC로 검색했을때 정렬되는것을 확인 할 수 있다.

### ORDER BY 절에서 별칭 사용  
![ORDER BY 별칭사용.png](sqldimg2%2FORDER%20BY%20%EB%B3%84%EC%B9%AD%EC%82%AC%EC%9A%A9.png)
