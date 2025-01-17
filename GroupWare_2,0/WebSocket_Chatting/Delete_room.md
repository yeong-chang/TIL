# 채팅 방 삭제

## DaoImpl 작성
```java
@Override
	public int DeleteChatRoom(int roomId) {
		int flag = 0;
		StringBuilder sb = new StringBuilder();
		ChatRoomVO vo = new ChatRoomVO();
		sb.append("DELETE FROM messenger \n");
		sb.append("WHERE chat_room_id = ? \n"); // chat_room_id를 기준으로 삭제

		Object [] args = {roomId};
		flag = this.jdbcTemplate.update(sb.toString(),args);

		return flag;
	}
}
```
DeleteChatRoom 메서드 작성 messenger테이블에서 삭제한 테이블을 chat_room_id가 일치하는 값만 삭제한다.

---

## Controller 작성
```java
	@PostMapping("deletechatroom.do")
	public String deleteChatRoom(@RequestParam("roomId") int roomIds) {
		try {
					chatRoomService.DeleteChatRoom(roomIds);
		} catch (Exception e) {
			e.printStackTrace();
			return "redirect:/chatroom/show.do"; // 오류 메시지를 전달하고 목록 페이지로 리다이렉트
		}
		System.out.println("Deleting room with ID: " + roomIds);
		return "redirect:/chatroom/show.do"; // 채팅방 삭제 후 채팅방 목록 페이지로 리다이렉트
	}
```
RequestParam으로 받아올 데이터를 roomId에 매핑해서 JSP에서 값을 받아온다.

---

## JSP 작성
```html
   <form action="deletechatroom.do" method="post">
            <table border="1" id="listTable" class="table">
                <thead>
                <tr>
                    <th class="table-head">선택</th>
                    <th class="table-head">방 번호</th>
                    <th class="table-head">ID 1</th>
                    <th class="table-head">ID 2</th>
                </tr>
                </thead>
                <tbody>
                <c:if test="${not empty chatRoomList}">
                    <c:forEach var="chatRoom" items="${chatRoomList}">
                        <tr title="더블클릭하면 상세 정보를 볼 수 있습니다.">
                            <td class="table-cell text-center">
                                <input type="radio" name="roomId" value="${chatRoom.roomId}">
                            </td>
                            <td class="table-cell text-center">${chatRoom.roomId}</td>
                            <td class="table-cell text-center">${chatRoom.senderId}</td>
                            <td class="table-cell text-center">${chatRoom.receiverId}</td>
                        </tr>
                    </c:forEach>
                </c:if>
                </tbody>
            </table>

            <div>
                <input type="submit" value="삭제">
            </div>
        </form>
```
form 에서 roomId 데이터를 받아오는 input타입을 radio로 roomId를 선택하도록 한다.

---

# 결과

채팅방 정보가 담긴 데이터베이스 SENDER_ID 9999, RECEIVE_ID 2006 이 담긴 정보 한건 있음
![채팅방 삭제 1.png](img%2F%EC%B1%84%ED%8C%85%EB%B0%A9%20%EC%82%AD%EC%A0%9C%201.png)

---

채팅방 목록 화면 에서 삭제할 방을 선택 해주고 삭제 버튼을 누른다
![채팅방 삭제 2.png](img%2F%EC%B1%84%ED%8C%85%EB%B0%A9%20%EC%82%AD%EC%A0%9C%202.png)

---

선택한 채팅방이 없어진것을 확인했다.
![채팅방 삭제 3.png](img%2F%EC%B1%84%ED%8C%85%EB%B0%A9%20%EC%82%AD%EC%A0%9C%203.png)

---

데이터베이스에 값이 완전히 지워진것을 확인.
![채팅방 삭제 4.png](img%2F%EC%B1%84%ED%8C%85%EB%B0%A9%20%EC%82%AD%EC%A0%9C%204.png)

---