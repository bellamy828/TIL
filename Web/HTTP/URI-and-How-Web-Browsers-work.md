# URI & How Web Browsers work

## What is URI, URL?

### URI(Uniform Resource Identifier)

- Locater, name 또는 둘다 추가로 분류될 수 있다.
- URL과 URN을 포함하는 상위 개념이다.
    - URL: Resource가 존재하는 위치를 지정한다.
    - URN: Resource에 이름을 부여한다.
    - URL(위치)는 변할 수 있지만 URN(이름)은 변하지 않는다.

### URL(Uniform Resource Loacation)

- URI의 실질적인 기능을 한다고 볼 수 있다.

> scheme://[userinfo@]host[:port][/path][?query][#fragment]
> 
- URL의 구조
    - Scheme
        - 주로 프로토콜을 사용한다.
            - Port: 자원에 접근할 때 통신 규약
                - ex. HTTP, HTTPS, FTP, …
            - Port는 생략 가능하다.
    - Userinfo
        - 인증을 위해서 사용자 정보를 포함할 때 사용하지만 거의 쓰지 않는다.
    - Host
        - Domain name, IP Address를 직접 사용할 수 있다.
    - Port
        - 일반적으로 생략, 생략했을 경우 HTTP는 80, HTTPS는 443을 사용한다.
    - Path
        - Resource 경로, 가급적 계층적 구조로 설계한다.
    - Query
        - key=value pairs 형태
        - ?로 시작, &로 query를 추가할 수 있다.
        - Server 입장에서 Parameter이자 String 형식이기 때문에 Query parameter / string이라고도 한다.
    - Fragment
        - HTML 내부 북마크와 같은 기능을 위해 사용하며 Server에 전송하는 데이터는 아니다.

## How Web Browsers work

### Web Browser Request

1. 주소창에 [google.com/search?q=java&hl=ko를](http://google.com/search?q=java&hl=ko를) 입력한다.
2. DNS 조회 후 해당 Domain의 IP address를 참조한다.
3. HTTP Request Mssage를 생성한다.
4. SOCKET library를 통해 DNS 조회 후 얻은 IP&Port로 3 way handshake하여 연결을 활성화한 후, OS 계층 TCP/IP로 데이터를 전달한다.
5. TCP/IP Packet을 생성하고, HTTP Message를 담아 Web으로 내보낸다.
6. 수많은 Nodes를 거쳐 목적지 Server에 도착하면 unpacking 후 message를 복원하고 process로 보낸다.
7. Server의 process는 HTTP Request Message에 대한 Response data를 가지고 HTTP Response Message를 생성한다.
8. Client가 Packet을 생성했던 것과 같이, Packet을 만들고 HTTP message를 담아 전송한다.
9. Client는 Response message를 unpack, data를 확인하여 Browser가 HTML을 렌더

<br>

Reference: https://www.inflearn.com/course/http-%EC%9B%B9-%EB%84%A4%ED%8A%B8%EC%9B%8C%ED%81%AC/
