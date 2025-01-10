## 관계의 개념
 
- 관계는 엔터티 간의 연관성을 나타낸것

### 관계의종류

1. 존재적 관계
   ex: 부서 엔터티가 삭제되면 사원 엔터티의 존재에 영향을 미침
2. 행위적 관계
   ex: 고객 엔터티의 행동에 의해 주문 엔터티가 발생

### 관계의 구성

1. 관계명
2. 차수
3. 선택성

### 관계의 차수

-한 엔터티의 레코드와 다른 엔터티의 레코드가 어떻게 연결되는지를 표현

1. 1대1관계
   -완전 1대1 관계
   ex:사원은 반드시 소속 부서가 있어야 함

   -선택적 1대1 관계

   ex:사원은 하나의 소속 부서가 있거나 아직 발령전이면 없을 수 있음

2. 1대N관계

   -하나의 행에 다른 엔터티의 값이 여러 개 있는 관계
   ex: 고객은 여러 개 계좌를 소유할 수 있음.

3. M대N의 관계
   -카테시안 곱이 발생한다
   ex: 한 학생이 여러 강의를 수강,보유 가능
   이 과정에서 구매이력이라는 엔터티가 필요 이것을 연결 엔터티라고 한다.

![sqld관계표기법.png](SQLDimg%2Fsqld%EA%B4%80%EA%B3%84%ED%91%9C%EA%B8%B0%EB%B2%95.png)

### 관계의 페어링

- 엔터티 안에 인스턴스가 개별적으로 관계를 가지는것
- 관계란 페어링의 집합이다

### 관계와 차수,페어링 차이

- 차수는 하나의 엔터티와 다른 엔터티 간의 레코드 연결 방식을 나타낸다.
- 페어링은 두 엔터티 간의 특정 연결을 설명한다.