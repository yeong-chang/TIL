# 채팅 방 생성

## DaoImpl 작성
```java
@Override
	public int CreateChatRoom(ChatRoomVO vo) {
		int flag = 0;
		StringBuilder sb = new StringBuilder(100);

		sb.append("INSERT INTO messenger (\n");
		sb.append("	    chat_room_id,     \n");
		sb.append("	    sender_id,        \n");
		sb.append("	    receiver_id       \n");
		sb.append("	) VALUES (            \n");
		sb.append("	    chat_room_no_seq.NEXTVAL, \n");
		sb.append("	    ?,                \n");
		sb.append("	    ?                 \n");
		sb.append("	)                     \n");

		Object [] args = {vo.getSenderId(),vo.getReceiverId()};
		flag = this.jdbcTemplate.update(sb.toString(),args);

		return flag;
	}

    
@Override
public List<UserVO> getAllUsers() {
    String sql = "SELECT USER_ID, USER_NAME FROM GW_USER";  // users 테이블에서 id와 name을 가져오는 SQL 쿼리

    // 쿼리를 실행하고 결과를 UserVO 객체로 매핑하여 리스트로 반환
    return jdbcTemplate.query(sql, (rs, rowNum) -> {
        UserVO user = new UserVO();
        user.setUserId(rs.getInt("USER_ID"));  // DB에서 id 값 가져오기
        user.setName(rs.getString("USER_NAME"));  // DB에서 name 값 가져오기
        return user;
    });
}
```


## Controller 작성
````java
@GetMapping("create_chatroom_index.do")
public String showChatRoomForm(Model model) {
    List<UserVO> userList = chatRoomService.getAllUsers(); // 유저 목록을 가져오는 서비스 호출
    model.addAttribute("userList", userList);  // userList를 모델에 추가
    return "chatroom/chatroom_reg";
}

@PostMapping("createChatRoom.do")
public String createChatRoom(@RequestParam("userId1") String userId1, HttpSession session) {
    // 세션에서 로그인한 유저의 ID를 받아오기
    UserVO user = (UserVO) session.getAttribute("user");

    // 받아온 값으로 채팅방 생성 로직 실행
    // 예를 들어, 채팅방 생성 서비스 호출
    try {
        // 서비스에서 채팅방 생성 로직 처리
        ChatRoomVO chatRoomVO = new ChatRoomVO();
        chatRoomVO.setSenderId(user.getUserId());  // 로그인한 사용자의 senderId
        chatRoomVO.setReceiverId(Integer.parseInt(userId1)); // 상대방의 userId1

        // 채팅방 생성 서비스 호출
        chatRoomService.CreateChatRoom(chatRoomVO);

    } catch (Exception e) {
        e.printStackTrace();
    }

    // 채팅방 생성 후 리다이렉트 또는 이동할 페이지로
    return "redirect:/chatroom/show.do";  // 채팅방 목록 페이지로 리다이렉트
}
````