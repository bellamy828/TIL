# 3. HTTP Basic

## HTTP(HyperText Transfer Protocol)

### HTTP 통신으로 가능한 작업

- HTML, Text 전송
- image, voice, video, file 전송
- JSON, [XML](https://ko.wikipedia.org/wiki/XML)(API)
- Server 간의 데이터 전송
- 거의 모든 형태의 데이터 전송

### 역사

- HTTP/0.9(1991년) → GET method 만 지원, HTTP header가 없었다
- HTTP/1.0(1996년) → Method, Header 추가
- HTTP/1.1(1997년) → 가장 많이 사용하며, 현재도 가장 영향력 있다.
- HTTP/2 (2015년) → 성능 개선
- HTTP/3 (개발중) → TCP 대신 UDP 사용, 성능 개선

### 기반 Protocol

- HTTP/1.1, HTTP/2 → TCP
- HTTP/3 → UDP
- 현재는 TCP 기반 HTTP/1.1을 주로 사용하지만 HTTP/2, HTTP/3의 비중도 점점 증가하고 있다.

### 특징

- Client ↔ Sever의 구조
    - Client → Server로 요청을 보내고, Server → Client 요청에 대한 응답을 보낸다.
    - Client와 Server의 개발을 분리할 수 있고, 각각 UI개발과 비즈니스 로직 개발에 집중할 수 있다.
- Stateless protocol
    - Server가 Client의 상태를 보존하지 않는다.
        - 장점
            - Server의 확장성이 높아진다(Scale out: 수평적 확장 ex. Server 장비 증설)
            - (Client가 매번 요청할 때마다 상태 정보를 제공하기 때문에)중간에 Server 장애가 발생해도 다른 Server에서 요청에 대한 응답 처리가 가능하다.
        - 단점: Client가 추가적으로 데이터 전송을 해야 한다.
        - 한계
            - 로그인과 같이 상태 정보가 필요한 기능이 분명히 있기 때문에 항상 무상태로 설계할 수는 없다.
            - 상태 유지는 최소한으로만, 꼭 필요할 때만 활용해야 한다.
- Connectionless
    - HTTP는 기본적으로 연결을 유지하지 않는 모델이다.
        - 장점
            - Client-Server가 필요한 순간에만 연결하여 Server의 자원을 효율적으로 사용할 수 있다.
        - 한계
            - 요청할 때 마다 다시 TCP/IP 연결을 해야한다(3 Way Handshake 시간 추가)
            - Web browser로 웹사이트에 방문하면 HTML 뿐만 아니라 JS, CSS, Images 등 수많은 자원을 함께 다운로드 해야 한다.
            - 현재는 HTTP Persistent Connections로 문제를 해결한다.
            - HTTP/2, HTTP/3에서 계속, 더 많이 최적화 중이다.
            - 같은 시각에 맞춰 발생하는 대용량 트래픽을 정상적으로 처리하기 위해서는 최대한 Stateless하게 설계하여 Server의 과부하를 막는 것이 관건이다.
- HTTP Message
    - 구조
        
        
        | start-line |
        | --- |
        | *( header-field CRLF ) |
        | CRLF |
        | [ message-body] |
        - start-line
            - Request Message
                
                > GET /search?q=http&hl=ko HTTP/1.1
                Host: www.google.com
                > 
                - HTTP Method  + ‘ ‘ + request-target + ‘ ‘ + HTTP-version + CRLF
                    - HTTP Method
                        - 종류
                            - GET
                            - POST
                            - PUT
                            - DELETE
                    - Request-target
                        - absolute-path[?query]
                        - “/”로 시작하는 경로
            - Response Message
                
                > HTTP/1.1 200 OK
                Content-Type: text/html;charset-UTF-8
                Content-Length: 3000
                
                <html>
                  <body>…</body>
                </html>
                > 
                - HTTP-version + ‘ ’ + status-code + ‘ ’ reason-phrase CRLF
                    - reason-phrase
                        - 사람이 이해할 수 있는 짧은 상태 코드 설명
        - header
            - header-field
                - field-name(대소문자 구분 없음) ”:” OWS(띄어쓰기 허용) field-value OWS
            - 용도
                - HTTP 전송에 필요한 모든 meta-data
                - 특정 Client-Server간 임의의 Header를 추가하는 것도 가능하다.
        - message-body
            - 실제 전송할 데이터
                - HTML 문서, 이미지, 영상, JSON등 byte로 표한할 수 있는 모든 데이터를 전송할 수 있다.
- 단순함과 확장 가능
    - HTTP message 형식도 단순하며, 확장 가능성이 큰 표준 기술이다.

<br>

Reference: https://www.inflearn.com/course/http-%EC%9B%B9-%EB%84%A4%ED%8A%B8%EC%9B%8C%ED%81%AC/
