## 문자 함수     
![문자형 함수.png](sqldimg2%2F%EB%AC%B8%EC%9E%90%ED%98%95%20%ED%95%A8%EC%88%98.png)
## 숫자 함수    
![숫자형 함수.png](sqldimg2%2F%EC%88%AB%EC%9E%90%ED%98%95%20%ED%95%A8%EC%88%98.png)
## 날짜 함수    
![날짜형 함수.png](sqldimg2%2F%EB%82%A0%EC%A7%9C%ED%98%95%20%ED%95%A8%EC%88%98.png)
## 변환 함수       
![변환 함수.png](sqldimg2%2F%EB%B3%80%ED%99%98%20%ED%95%A8%EC%88%98.png)

## 그룹 함수
(NULL 무시하고 연산)
(COUNT의 경우 모든값이 NILL일때는 0을 리턴해줌) 

| 함수명 | 함수기능 | 사용예시 |
| --- | --- | --- |
| COUNT(대상) | 행의 수 리턴 | SELECT COUNT(SAL) FROM EMP; |
| SUM(대상) | 총 합 리턴 | SELECT SUM(SAL) FROM EMP; |
| AVG(대상) | 평균 리턴  | SELECT AVG(SAL) FROM EMP; |
| MIN(대상) | 최솟값 리턴  | SELECT MIN(SAL) FROM EMP; |
| MAX(대상) | 최댓값 리턴  | SELECT MAX(SAL) FROM EMP; |
| VARIANCE(대상) | 분산 리턴 | SELECT VARIANCE(SAL) FROM EMP; |
| STDDEV(대상) | 표준편차 리턴  | SELECT STDDEV(SAL) FROM EMP; |

## 일반함수

| 함수명  | 함수기능                                          | 사용예시 |
| --- |-----------------------------------------------| --- |
| DEDODE(대상, 값1 ,리턴1 , 값2, 리턴2 , 그외 리턴 ) | 대상의 값이1이면 리턴1, 값이 2이면 리턴2, 값이 그 외라고 그외 리턴     |  |
| NVL(대상,치환값) | 대상이 NULL이면 치환값으로 치환하여 리턴                      |  |
| NVL2(대상,치환값1,치환값2) | 대상이 NULL이면 치환값2로 치환 NULL이 아니면 치환값 1로 치환하여 리턴  |  |
| COALESCE(대상1,대상2,그외리턴) | 대상들 중 널이 아닌값 출력 (가장 첫 번째 부터) 모두 NULL이면 그외값 리턴 |  |
| NULLIF(대상1,대상2) | 두 값이 같으면 NULL, 두값이 다르면 대상1 리턴                 |  |
| CASE | 조건별 치환 및 연산 수행                                |   |

### DECODE 사용 예제  
![DECODE예제.png](sqldimg2%2FDECODE%EC%98%88%EC%A0%9C.png)

### NVL, NVL2 사용 예제  
![NVL_NVL2예제.png](sqldimg2%2FNVL_NVL2%EC%98%88%EC%A0%9C.png)

### COALESCE 사용 예제  
![COALESCE예제.png](sqldimg2%2FCOALESCE%EC%98%88%EC%A0%9C.png)

### NULLIF 사용 예제  
![NULLIF예제.png](sqldimg2%2FNULLIF%EC%98%88%EC%A0%9C.png)

### CASE 사용 예제    
![CASE문예제.png](..%2FSQLD%20sub2%2Fsqldimg2%2FCASE%EB%AC%B8%EC%98%88%EC%A0%9C.png)
