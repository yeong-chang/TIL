# HttpSession
- 로그인한 계정의 세션값을 불러오기
HttpSession은 서버 측에서 클라이언트의 상태를 저장하는 객체입니다.
주로 사용자의 로그인 상태나 사용자 정보를 세션에 저장하고, 그 정보를 여러 요청에서 유지하는 데 사용됩니다.


- 세션에서 로그인한 사용자 정보 가져오기
로그인한 사용자의 정보를 HttpSession에서 불러오는 방법은
로그인 성공 시, 사용자의 정보를 HttpSession에 저장하고, 이후에 그 정보를 불러와서 사용할 수 있습니다.

## session 값을 불러온 예제 코드

### session 생성
```java
@PostMapping(value = "login.do")
	@ResponseBody 
	public String login(UserVO user, HttpSession httpSession) throws SQLException{
		String jsonString = "";
        
        // 로그인 로직
         UserVO outVO = loginService.doSelectOne(user);
    
			//session 생성
			httpSession.setAttribute("user", outVO);
            
		return jsonString;
	}
```
<mark>"user"라는 이름으로 로그인한 세션을 저장함</mark>

### controller
```java
	@GetMapping("show.do")
	public String ShowChatRoom(Model model,HttpSession session) {
		String viewName = "chatroom/chatroom_list";
		UserVO user = (UserVO) session.getAttribute("user");
		try {
			List<ChatRoomVO> chatRoomList = chatRoomService.ShowChatRoom(user.getUserId());
			model.addAttribute("chatRoomList", chatRoomList);
		} catch (Exception e) {
			e.printStackTrace();
		}
		return viewName;
	}
```
<mark>저장 되어있는"user"세션을 사용해서 UserId가 일치하는 값만 보여주도록 함</mark>

### VO
```java
package com.pcwk.ehr.user.domain;

import com.pcwk.ehr.cmn.DTO;

public class UserVO extends DTO {

    private int userId; //사용자 ID

    public int getUserId() {
        return userId;
    }
    public void setUserId(int userId) {
        this.userId = userId;
    }
}
```