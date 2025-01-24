# RowMapper

## 코드

```java
 new RowMapper<ChatRoomVO>() {
    @Override
    public ChatRoomVO mapRow(java.sql.ResultSet rs, int rowNum) throws java.sql.SQLException {
        // ResultSet 값을 ChatRoomVO 객체에 저장
        ChatRoomVO chatRoomVO = new ChatRoomVO();
        chatRoomVO.setRoomId(rs.getInt("chat_room_id"));
        chatRoomVO.setSenderId(rs.getInt("sender_id"));
        chatRoomVO.setReceiverId(rs.getInt("receiver_id"));
        return chatRoomVO;
    }
```

- RowMapper는 데이터베이스에서 가져온 데이터를 JAVA객체로 변환하는 인터페이스이다.  
- SQL 쿼리에서 반환된 컬럼명을 자바 클래스의 필드에 매핑하는 작업을 중앙 집중화하여 관리할 수 있습니다.

---

## RowMapper 장점
- 데이터베이스에서 가져온 값이 많을 경우 1행 마다 반복문을 통해 직접 매핑해야하는데,  
RowMapper를 사용하면 쿼리 결과를 Java 객체로 자동으로 매핑해 주므로 코드가 간결하고 유지보수가 용이하다.

