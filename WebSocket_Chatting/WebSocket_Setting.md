 # WebSocket_Chatting 
 
## WebSocket 이란?
- 웹 소켓(WebSocket)은 HTML5 표준 중 하나로, 클라이언트(웹 브라우저)와 서버 간에 양방향 통신을 가능하게 하는 프로토콜입니다.
기존의 HTTP 통신과는 다르게, 연결이 지속적으로 열려 있어 실시간 데이터 전송에 적합합니다.

## WebSocket의 주요 특징
1. 양방향 통신이 가능하다.
2. 지속적인 연결이 가능하다.
3. 실시간 데이터 전송이 가능하다.

## HTTP 통신과의 차이
| 특징 | HTTP | WebSocket |
| -- | --- | --- |
| 통신 방식 | 단방향(클라이언트 → 서버) | 양방향(Full-Duplex) |
| 연결 방식 | 요청-응답 반복 | 한 번 연결 후 지속 유지 |
| 프로토콜 | HTTP | WebSocket (ws:// 또는 wss://) |
| 사용 사례 | 전통적인 웹 요청(HTML, API 등) | 실시간 채팅, 주식 시세, 게임 등 |

## spring-websocket , spring-messaging pom추가

Spring 프로젝트 내에서 버전 일치를 관리하기 위해  
<mark><version>${org.springframework-version}</version></mark>로 설정
```xml     
        <!-- https://mvnrepository.com/artifact/org.springframework/spring-websocket -->
		<dependency>
			<groupId>org.springframework</groupId>
			<artifactId>spring-websocket</artifactId>
			<version>${org.springframework-version}</version>
		</dependency>

        <!-- https://mvnrepository.com/artifact/org.springframework/spring-messaging -->
		<dependency>
			<groupId>org.springframework</groupId>
			<artifactId>spring-messaging</artifactId>
			<version>${org.springframework-version}</version>
		</dependency>
```

## servlet-context.xml 설정
```xml
<!--name space 추가-->
 xmlns:websocket="http://www.springframework.org/schema/websocket"

<!--schemaLocation 추가-->
 xsi:schemaLocation="http://www.springframework.org/schema/websocket http://www.springframework.org/schema/websocket/spring-websocket-4.3.xsd



<!-- Websocket and STOMP messaging -->
	<websocket:message-broker application-destination-prefix="/ehr">
		<!-- Configure STOP endpoint -->
		<websocket:stomp-endpoint path="/ws">
			<websocket:sockjs/>
		</websocket:stomp-endpoint>

		<!-- Broker -->
		<websocket:simple-broker prefix="/topic"/>

	</websocket:message-broker>
```

## web.xml 설정
- 모든 url정보를 사용할수있게씀 <url-pattern>/</url-pattern>수정 
```xml
<servlet-mapping>
      <servlet-name>appServlet</servlet-name>
      <url-pattern>/</url-pattern>
</servlet-mapping>
```