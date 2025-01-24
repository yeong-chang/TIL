# ReqestParam Aunotation

- @RequestParam은 HTTP 요청에서 필요한 form데이터를 메서드의 파라미터와 바인딩하기 위해 사용합니다.
- 여러 파라미터를 동시에 처리 할 수있습니다.
- defaultValue, readonly, required 등을 사용해서 파라미터값을 자동 설정 할 수 있다.

## 사용 예

### Controller

```java
@PostMapping("deletechatroom.do")
	public String deleteChatRoom(@RequestParam("roomId") int roomId) {
		try {
					chatRoomService.DeleteChatRoom(roomId);
		} catch (Exception e) {
			e.printStackTrace();
			return "redirect:/chatroom/show.do"; // 오류 메시지를 전달하고 목록 페이지로 리다이렉트
		}
		System.out.println("Deleting room with ID: " + roomId);
		return "redirect:/chatroom/show.do"; // 성공적으로 삭제 후 채팅방 목록 페이지로 리다이렉트
	}
```

쿼리문에서 필요한 파라미터를 roomId로 바인딩.

---

### DAOImpl

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
```

쿼리문에서 필요한 파라미터 chat_room_id 하나이다.
클라이언트에서 받을 데이터를 roomId라는 변수로 받고 이를 args배열에 저장 jdbcTemplate.update를통해 
파라미터를 받고 반환한다.

---

### JSP

```html
<form action="deletechatroom.do" method="post">
    <input type="radio" name="roomId" value="${chatRoom.roomId}">
</form>
```

input타입의 클라이언트 데이터를 Controller에서 바인딩했던 변수인 roomId로 맞춰주고 
값을 roomId로 받아준다.