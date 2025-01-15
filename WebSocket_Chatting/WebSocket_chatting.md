# WebSocket_Chatting 

## Controller
```java
@Controller
public class ChatController {

    final Logger log = LogManager.getLogger(getClass());

    public ChatController() {
        log.debug("┌───────────────────────────────────────┐");
        log.debug("│ ChatController                        │");
        log.debug("└───────────────────────────────────────┘");
    }
    
    @GetMapping("/chat_index.do")
    public String chat() {
        String viewname = "chat/chat";
        log.debug("┌───────────────────────────────────────┐");
        log.debug("│ ChatController                        │");
        log.debug("└───────────────────────────────────────┘");
        return viewname;
    }
    @MessageMapping("/sendMessage.do") //클라이언트에서 /app/chat로 메시지 전송시 사용
    @SendTo("/topic/messages.do")//구독중인/topic/messages.do로 메시지 브로드 케스트
    public ChatMessage sendMessage(ChatMessage message) {
        log.debug("message"+message);
        message.setContent("이름:"+message.getContent());

        log.debug("message"+message);
    return message;
    }
}
```

## VO 
```java
public class ChatVO {

    private String sender;
    private String content;

    public ChatMessage() {
        super();
    }

    public String getSender() {
        return sender;
    }

    public void setSender(String sender) {
        this.sender = sender;
    }

    public String getContent() {
        return content;
    }

    public void setContent(String content) {
        this.content = content;
    }

    @Override
    public String toString() {
        return "ChatMessage{" +
                "sender='" + sender + '\'' +
                ", content='" + content + '\'' +
                '}';
    }
}

```

## HTML
```html
<div id="chat">
    <h2>Chat</h2>
    <div id="message"></div>
    <div id="input">
        <input type="text" id="messageInput" placeholder="메세지를 입력하세요">
        <button onclick="sendMessage();">Send</button>
    </div>
</div>
```

## javaScript
```javascript
<script>
    let stompClient = null;

    // 웹소켓 연결
    function connect() {
        const socket = new SockJS('/ehr/ws');
        stompClient = Stomp.over(socket);
        stompClient.connect({}, function(frame) {
            console.log('Connected: ' + frame);

            // 구독 : /topic/messages.do
            stompClient.subscribe('/topic/messages.do', function(message){
                console.log(message);
                // 받은 메시지를 화면에 표시
                showMessage(JSON.parse(message.body));
            });
        });
    }
    function showMessage(message) {
        const messageDiv = document.getElementById('message');
        const messageElement = document.createElement('div');
        messageElement.textContent = message.sender + ": " + message.content;
        messageDiv.appendChild(messageElement);
        messageDiv.scrollTop = messageDiv.scrollHeight;
    }
    // 메시지 전송
    function sendMessage() {
        const messageContent = document.getElementById('messageInput').value.trim();

        if (messageContent && stompClient) {
            // 메시지 전송
            stompClient.send('/ehr/sendMessage.do', {}, JSON.stringify({
                sender: '이름',
                content: messageContent
            }));
            document.getElementById('messageInput').value = '';
        }
    }
    window.onload = function() {
        connect();
    };
</script>
```
