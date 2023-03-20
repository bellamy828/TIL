# Cookies
## what is a Cookie?
> HTTP는 Stateless protocol이다.<br>
따라서 Client-Server가 Request와 Response를 주고 받으면 연결이 끊어진다.<br>
Clinet가 다시 요청하면 Server는 이전 요청을 기억하지 못한다.<br>
Client-Server는 서로의 상태를 유지하지 않는다.
> 
### Client vs Server
  - Request header
    - Cookie: Client가 Server에서 받은 Cookies를 저장하고 HTTP 요청할 때 Server로 전달한다.
  - Response header
      - Set-Cookie: Server에서 Clinet로 Cookie를 전달한다.
### 자주 사용되는 용도

   - 주로 사용자 로그인 세션 관리를 위해서 사용한다.
   - 최근 광고 정보 트래킹을 위해서 많이 사용한다.
   - 보안에 민감한 데이터는 저장하지 않는다.
   - Cookie의 정보는 항상 Server에 전송된다.
     - 추가적인 네트워크 트래픽이 발생하기 때문에, 정말 필요한 최소한의 정보만 사용한다.
        - Session ID
        - Tokens
     - Web storage(Local, Session Storage등)을 사용하여 Server에 전송하지 않고, Web browser 내부에 데이터를 저장하는 방법도 있다.
## Life time
### 영속 쿠키
  - expires=Sat, 18-Mar-2023 01:16L21 GMT
      - 만료일이 되면 쿠키가 삭제된다.
  - max-age=3600(seconds)
      - 0, 음수를 지정하면 쿠키가 삭제된다.
### 세션 쿠키
  - 만료 날짜를 생략하면 Browser 종료하기 전 까지만 유지한다.

## Attributes
### Domain
  - domain=google.com과 같이 명시하면 서브 도메인 까지 접근할 수 있고, 명시하지 않으면 서브 도메인에는 접근할 수 없다.
### Path
  - path=/home과 같이 명시하면 /home/leve1/leve2/… 하위 경로 까지만 쿠키 접근이 가능하다.
  - 일반적으로는 root 페이지로 지정한다.
### Secure
  - 쿠키는 http/https 구분하지 않고 전송하는데 Secure를 적용하면 https인 경우에만 전송한다.
### HttpOnly
  - [XSS](https://ko.wikipedia.org/wiki/%EC%82%AC%EC%9D%B4%ED%8A%B8_%EA%B0%84_%EC%8A%A4%ED%81%AC%EB%A6%BD%ED%8C%85) 공격 방지용, JS로 접근 불가하도록 하고, HTTP 전송에만 사용되도록 한다.
### SameSite
  - [XSRF](https://ko.wikipedia.org/wiki/%EC%82%AC%EC%9D%B4%ED%8A%B8_%EA%B0%84_%EC%9A%94%EC%B2%AD_%EC%9C%84%EC%A1%B0) 공격 방지용, 요청 Domain과 Cookie에 설정된 Domain이 같은 경우만 Cookie를 전송해준다.

<br>

Reference: https://www.inflearn.com/course/http-%EC%9B%B9-%EB%84%A4%ED%8A%B8%EC%9B%8C%ED%81%AC#
