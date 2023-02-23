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

### HTTP Status code

- Client HTTP 요청에 대한 Server의 응답 코드로 성공/실패 여부를 알 수 있다.
- Client는 Server로 부터 받은 Status code를 토대로 적절한 대응을 하게 된다.
- 100번대 부터 500번대 까지 총 5개의 클래스로 구분하여 대략적인 응답 내용을 파악할 수 있다.
    - 1xx(정보): 요청을 받았으며 작업을 계속한다.
    - 2xx(성공): 클라이언트가 요청한 동작을 성공적으로 수신하여 이해했고 성공적으로 처리했다.
    - 3xx(리다이렉션): 요청을 완료하기 위해 추가 작업 조치가 필요하다.
    - 4xx(클라이언트 오류): 클라이언트의 요청에 문제가 있다.
    - 5xx(서버 오류): 서버가 유효한 요청의 수행을 실패했다.
- 자주 사용하는 Status code
    
    | code | status | desc  |
    | --- | --- | --- |
    | 200 | OK | 요청 성공(ex. 잔액 조회) |
    | 201 | Created | 리소스 생성 성공(ex. 게시글 작성, 회원 가입) |
    | 400 | Bad Request | 데이터의 형식이 올바르지 않는 등 서버가 요청을 이해할 수 없음 |
    | 401 | Unauthorized | 인증되지 않은 상태에서 인증이 필요한 리소스에 접근했을 때(ex. 로그인 하지 않고 사용자 정보 요청) |
    | 403 | Forbidden | 인증된 상태에서 권한이 없는 리소스에 접근했을 때 (ex. 일반 유저가 관리자 메뉴 접근) |
    | 404 | Not Found | 요청한 Route가 없거나 찾는 리소스가 없을 때 |
    | 500 | Bad Gateway | 서버에서 예상하지 못한 에러가 발생햇을 때(ex. 예외 처리를 하지 않아 오류 발생) |

<br>

## How the web works?

### 브라우저 주소창에 google.com을 입력하고 웹 페이지가 보여지는 과정

1. Browser 주소창에 URL(www.google.com)을 입력하면 HTTP Request message를 생성한다.
2. DNS Lookup을 통해 해당 Domain의 Server IP주소를 알아낸다.
3. 반환된 IP주소(Google Server IP)로 HTTP Request message 전송 요청 한다.
    1. 생성된 HTTP Request message를 TCP/IP 층에 전달한다.
    2. HTTP 요청 메시지에 Header를 추가해서 TCP/IP 패킷을 생성한다.
4. 해당 패킷은 전기신호로 랜선을 통해 네트워크로 전송되고, 목적지 IP에 도달한다.
5. 구글 Server에서 도착한 패킷을 Unpack, message를 복원하고 Server의 Process로 보낸다.
6. Server의 Process는 HTTP Request message에 대한 Response data를 가지고 HTTP Response message를 생성한다.
7. HTTP Response message를 전달 받은 방식 그대로 Client IP로 전송한다.
8. HTTP Response message에 담긴 데이터를 토대로 웹 브라우저에서 HTML Render, Google의 홈화면이 보여진다.

[^1]:Parmeter / Query string: 일반적으로는 파라미터는 특정 id 나 이름을 가지고 조회를 할 때 사용하고, 쿼리의 경우엔 어떤 키워드를 검색하거나, 요청을 할 때 필요한 옵션을 전달 할 때 사용된다

<br>

Reference: https://www.nossi.dev/interview/cs/network
