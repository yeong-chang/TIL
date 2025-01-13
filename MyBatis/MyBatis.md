# MyBatis 사용

## BoardMapper
- 파일 위치 <mark>src/main/java/com/pcwk/ehr/mapper/BoardMapper</mark>  
![Boardmapper위치.png](img%2FBoardmapper%EC%9C%84%EC%B9%98.png)
```java
package com.pcwk.ehr.mapper;

@Mapper
public interface BoardMapper {
	//게시판 조회
    List<BoardVO> selectAllBoard() throws SQLException;
}

```

## BoardService
```java
@Service
public class BoardService {

    @Autowired
    private BoardMapper boardMapper;

    public List<BoardVO> selectAllBoard() throws SQLException {
       return boardMapper.selectBoard();
    }
}
```

## BoardController
```java
@RestController
@RequestMapping("/board")
public class BoardController {

    @Autowired
    private BoardService boardService;

    @GetMapping("/selectAll")
    public ResponseEntity<List<BoardVO>> selectBoard() throws SQLException {
        boardService.selectAllBoard();
        if (boards.isEmpty()) {
            return ResponseEntity.noContent().build();
        }
        return ResponseEntity.ok(boards);
    }
}
```

## 정리 

<mark>1. mybatis-config.xml 설정.</mark> - MyBatis의 전역 설정.  
<mark>2. boardMapper.xml 설정.</mark> - SQL 쿼리와 결과 매핑 정의.  
<mark>3. BoardMapper 인터페이스 생성.</mark> -SQL 매핑 메서드 정의.  
<mark>4. BoardService 클래스 생성.</mark> - 비즈니스 로직 처리 및 Mapper 호출.  
<mark>5. BoardController 클래스에 Service 의존성을 주입하고 사용.</mark> - 클라이언트 요청 처리 및 서비스 호출.  