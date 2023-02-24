# Cookie & Session

## Why we use Cookie and Session?

### connectionless & stateless

- HTTP 통신은 Client의 Request가 Server에 전달되고 그에 맞는 Response를 보낸 후 연결을 끊고, 상태 정보 또한 사라진다.
- Request Header에 ‘keep-alive’ 값을 통해 Connection을 끝내지 않고 유지할 수도 있다.

## What are Cookie and Session?

### Cookie

- Client(Browser) 측, Local에 저장되는 데이터 파일(key-value pair)이다.
- Browser를 종료해도 유효기간 동안 유지된다.
- Server에서 Response Header에 set-cookie 속성을 사용해서 클라이언트에 쿠키를 만들고, 사용자가 따로 작업을 하지 않아도 Browser가 Request Header에 Cookie를 담아 전송한다.
    1. Client의 요청을 받은 Server가 Client 정보를 토대로 Cookie를 구성한다.
    2. Server가 Response Header에 Cookie를 담아 보낸다.
    3. Response를 받은 Client, Browser가 Cookie를 Cookie directory에 저장한다.   

### Session

- Client를 구분하기 위해 각 Client에게 Session ID를 부여하고, Client는 Cookie에 Session ID를 저장한다.
- 사용자 정보는 Server에 저장/관리 한다.
- 유효기간을 설정하여 응답이 없다면 끊을 수 있고, Browser를 종료할 때 까지 인증 상태를 유지할 수 있다.
- Cookie 보다 보안 측면에서 안전할 수는 있지만, Server 자원을 사용하기 때문에 Request가 많을 경우 과부하나 성능 저하의 요인이 될 수 있다.

<br>

Reference: https://www.nossi.dev/interview/cs/network
