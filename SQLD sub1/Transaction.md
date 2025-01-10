## 트랜잭션 

- 트랜잭션이란 데이터베이스의 상태를 변화시키기 위해 수행하는 작업의 단위를 뜻한다.   
- DML 
1. SELECT
2. INSERT
3. DELETE
4. UPDATE
주로 DML을 사용해서 데이터베이스에 접근할때 트랜잭션이 이루어진다

### 트랜잭션이란
- 트랜잭션은 데이터베이스에서 수행되는 하나 이상의 작업을 논리적 단위로 묶은 것이다.
트랜잭션 내에서 수행된 작업은 모두 성공하거나 모두 실패해야 한다.

예) 내가 친구 1 에게 송금을 보내는 상황이다.    
    만약 내가 송금을 했는데 친구 1이 입금 받지 못하는 상황이 발생 하면 안되므로  
    트랜잭션 처리가 필요 한 것이다.

### 트랜잭션의 특징(ACID)
- Atomicity(원자성)
  모두 반영되던가, 모두 반영되지 않아야 한다.
- Consistency(일관성)
  트랜잭션의 작업 처리 결과가 항상 일관성이 있어야 한다.
- Isolation(고립성)  
  트랜잭션이 여러개가 이루어 지고있을때 서로 영향을 미쳐서는 안된다.
- Durability(영속성)
  트랜잭션이 성공적으로 완료되었을 경우 영구적으로 반영되어야 한다.