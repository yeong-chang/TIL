# RowMapper_Interface

## 사용 코드
```java
@Override
	public List<ChatRoomVO> ShowChatRoom(int userId) {

		// SQL 쿼리 작성
		StringBuilder sb = new StringBuilder(100);
		sb.append("SELECT chat_room_id, sender_id, receiver_id \n");
		sb.append("FROM messenger \n");
		sb.append("WHERE sender_id = ? OR receiver_id = ? \n");  // sender_id나 receiver_id가 일치하는 경우
		sb.append("ORDER BY chat_room_id ASC \n");

		// SQL 쿼리를 실행하고 결과를 ChatRoomVO 객체 리스트로 매핑
		List<ChatRoomVO> chatRoomList = jdbcTemplate.query(sb.toString(), new Object[] { userId, userId }, new RowMapper<ChatRoomVO>() {
			@Override
			public ChatRoomVO mapRow(ResultSet rs, int rowNum) throws java.sql.SQLException {
				ChatRoomVO chatRoomVO = new ChatRoomVO();
				chatRoomVO.setRoomId(rs.getInt("chat_room_id"));
				chatRoomVO.setSenderId(rs.getInt("sender_id"));
				chatRoomVO.setReceiverId(rs.getInt("receiver_id"));
				return chatRoomVO;
			}
		});
		return chatRoomList;  // List<ChatRoomVO> 반환
	}
```


## RowMapper 인터페이스

![RowMapper인터페이스.png](img%2FRowMapper%EC%9D%B8%ED%84%B0%ED%8E%98%EC%9D%B4%EC%8A%A4.png)

위처럼 RowMapper 인터페이스는 mapRow 메서드가 있고 

채팅방을 생성해 DB에 저장하는 메서드이다.  
여기서 new RowMapper<ChatRoomVO>() 는 왜 사용하는것 일까?


## 사용이유
RowMapper 를 사용하기전 JDBC를 사용했을때엔 쿼리문에서 나온 정보를 하나하나 뽑아서 배열에 저장을 했었는데
RowMapper를 사용하면 


## RowMap 사용하지 않았을떄
```java
ResultSet rs = stat.excuteQuery("SELECT * FROM USER");

while(rs.next()) {
     // user 객체에 값 저장
     user = new User();
     user.setId(rs.getInt(1));
     user.setName(rs.getString(2));
     user.setDescription(rs.getString(3));
     
     // 리스트에 추가
     userList.add(user);
}
```

---