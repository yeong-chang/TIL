## 스키마

- DB의 구조와 제약 조건에 관한 전반적인 명세를 기록하는 계정?
- 나는 스키마를 계정? 디렉토리? 와 유사하다고 생각한다.(구조적 틀 이라고 생각함)

**데이터베이스 스키마 구조 3단계**

| **항목** | **내용** | **비고** |
| --- | --- | --- |
| **외부스키마(External Schema)** | -사용자 관점에서 데이터베이스 스키마를 정의
-사용자나 응용 프로그램이 필요한 데이터를 정의  | 사용자 관점접근하는 특성에 따른 스키마 구성 |
| **개념스키마(Conceptual Schema)** | - 모든 사용자 관점을 통합한 조직 전체의 DB를 기술하는 것- 모든 응용시스템들이나 사용자들이 필요로 하는 데이터를 통합한 조직 전체의 DB를 기술한 것으로 DB에 저장되는 데이터와 그들간의 관계를 표현하는 스키마 | 통합관점 |
| **내부스키마(Internal Schema)** | - DB가 물리적으로 저장된 형식
- 물리적 장치에서 데이터가 실제적으로 저장되는 방법을 표현하는 스키마 | 물리적 저장구조 |

### 스키마의 독립성

1. 논리적독립성
2. 물리적독립성