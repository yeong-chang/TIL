## GROUP BY절 

- 각 행을 특정 조건에 따라 그룹으로 분리하여 계산하도록 하는 구문식
- 그룹에 대한 조건은 WHERE절에서 사용할 수 없음
- GROUP BY절을 사용하면 데이터가 요약되므로 요약되기 전 데이터와 함께 출력할 수 없음

#### GROUP BY절 사용 예제    
![GROUP BY 사용예제.png](sqldimg2%2FGROUP%20BY%20%EC%82%AC%EC%9A%A9%EC%98%88%EC%A0%9C.png)

#### GROUP BY절 잘못된 사용 예제  
![GROUP BY절 잘못된 사용 예제.png](sqldimg2%2FGROUP%20BY%EC%A0%88%20%EC%9E%98%EB%AA%BB%EB%90%9C%20%EC%82%AC%EC%9A%A9%20%EC%98%88%EC%A0%9C.png)  
GROUP BY 절을 사용할 경우에는 집계된 정보만 출력이가능하다.  
위와 같이 ENAME은 집계되지 않은 정보 이기 때문에 출력이 불가능하다.

### HAVING 절
- 그룹 함수 결과를 조건으로 사용할 때 사용하는 절

#### HAVING을 사용하지 않았을때   
![HAVING 안쓰인 예제.png](sqldimg2%2FHAVING%20%EC%95%88%EC%93%B0%EC%9D%B8%20%EC%98%88%EC%A0%9C.png)
  
#### HAVING을 사용한 예제  
![HAVING사용예제.png](sqldimg2%2FHAVING%EC%82%AC%EC%9A%A9%EC%98%88%EC%A0%9C.png)

#### WHERE 절과 HAVING 절을 모두 사용할 때
- 쉽게 생각하면 WHERE절로 먼저 필터링하고 GROUP BY절을 사용하고 HAVING절에서 그룹함수 결과를 사용해 검색하는데 성능상 좋다.

![WHERE_HAVING.png](sqldimg2%2FWHERE_HAVING.png)
