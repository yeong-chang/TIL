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

getAllUsers()메서드는 채팅방을 생성할때 수신받는 사람의 ID값을 불러올때 선택하기 위해 
모든 사용자의 ID와 NAME 정보를 받아온다.

---

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
로그인한 사용자의 아이디를 senderId로 받기 위해 session값을 사용한다.  
RequestParam으로 받아올 데이터를 userId1에 매핑해서 JSP에서 값을 받아온다.

---

## JSP 작성
```html
<body>
<jsp:include page="/WEB-INF/views/include/header.jsp"></jsp:include>
<jsp:include page="/WEB-INF/views/include/aside.jsp"></jsp:include>

<div class="container">
    <h1>채팅방 생성</h1>
    <div class="form-container">
        <form action="createChatRoom.do" method="post">
            <div>
                <label for="userId1">유저 1</label>
                <select name="userId1" id="userId1">
                    <option value="">유저를 선택하세요</option>
                    <c:forEach var="user" items="${userList}">
                        <option value="${user.userId}">${user.name}</option>
                    </c:forEach>
                </select>
            </div>


            <div class="buttons">
                <input type="submit" id="doCreate" value="등록">
                <input type="button" id="moveToPrevious" value="돌아가기" onclick="window.history.back();">
            </div>
        </form>
    </div>
</div>

</body>
```

select 태그의 id를 userID1로 매핑해주고 선택해주는 값의 userId를 Controller로 넘긴다.

---

# 결과
채팅방 등록하는 초기 화면.
![채팅방 생성 1.png](img%2F%EC%B1%84%ED%8C%85%EB%B0%A9%20%EC%83%9D%EC%84%B1%201.png)

---

채팅방에 초대할 사람의 이름을 선택하는 화면. (홍주영 선택)
![채팅방 생성 2.png](img%2F%EC%B1%84%ED%8C%85%EB%B0%A9%20%EC%83%9D%EC%84%B1%202.png)

---

로그인한 아이디와 홍주영의 아이디가 들어가있는 채팅방 생성.
![채팅방 생성 3.png](img%2F%EC%B1%84%ED%8C%85%EB%B0%A9%20%EC%83%9D%EC%84%B1%203.png)

---

홍주영 USER_ID 확인 2006 맞게 들어왔다.
![채팅방 생성4.png](img%2F%EC%B1%84%ED%8C%85%EB%B0%A9%20%EC%83%9D%EC%84%B14.png)

---
