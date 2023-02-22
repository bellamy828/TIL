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

### HTTP Requsest Method

- GET: 리소스 조회
    - Client가 Server에게 정보를 요청할 때 사용하는 Method
    - Parameter / Query string(Key-value pair)[^1]을 포함하여 전송한다.
    - Cache가 가능해서 Server에 GET 요청을 하면 Browser가 그 결과를 저장하고 이후 동일한 요청을 저장된 값으로 가져올 수 있다.
- POST: 요청 데이터 처리(주로 생성)
    - Client가 데이터를 Body에 담아 전송, Server가 해당 요청을 처리하도록 한다.
    - 생성 외에도 변경이나 특정 프로세스를 처리하기도 한다.
- PUT: 리소스를 아예 대체, 해상 리소스가 없으면 생성
- PATCH: 리소스의 일부분을 수정

[^1]:Parmeter / Query string: 일반적으로는 파라미터는 특정 id 나 이름을 가지고 조회를 할 때 사용하고, 쿼리의 경우엔 어떤 키워드를 검색하거나, 요청을 할 때 필요한 옵션을 전달 할 때 사용된다

<br>

Reference: https://www.nossi.dev/interview/cs/network
