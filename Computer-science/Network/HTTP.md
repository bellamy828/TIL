# HTTP

## What is HTTP?

### HTTP(HyperText Transfer Protocol)

- 웹 상에서 정보를 전송하기 위한 통신 Protocol, HTML과 같은 문서를 전송하기 위해 사용되는 규약이다.
    - Client → Server HTTP Request 전송
        - Request message
            - Start line(Method, Path, HTTP version), Headers, Body
    - Server → Client HTTP Response 전송
        - Response message
            - Status line(HTTP version, Status code, Status message), Headers, body
- 서버에 연결 후 요청에 응답을 받으면 연결을 끊어버리는 Connectionless 특성을 갖는다.
    - 많은 사람들이 웹에서 요청을 보내더라도 동시 접속을 최소화하고 많은 요청을 처리할 수 있다.
    - 대신 클라이언트의 이전 상태를 알 수 없는 Stateless 특성 또한 갖게 된다.
        - Cookie, Session, Token등을 활용해 정보 저장, 로그인 문제를 해결할 수 있다.
- 정보를 Text 형식으로 주고받기 때문에 intercept 데이터 유출을 막기 위해 암호화를 추가한 HTTPS가 도입되었다.

<br>

Reference: https://www.nossi.dev/interview/cs/network
