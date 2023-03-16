# HTTP Headers

## HTTP headers

### 용도

- HTTP 전송에 필요한 모든 부가정보
    - ex. 메시지 바디의 내용, 바디의 크기, 압축, 인증, 요청 Client, Server 정보, Cache 관리 정보…
- 표준 헤더가 무수히 많다.
- 필요시 임의의 header도 추가 가능하다.

### 과거 헤더 분류(RFC2616)

- General headers: 메시지 전체에 적용되는 정보
    - ex. Connection: close
- Request headers: 요청 정보
    - ex. User-Agent: Mozilla/5.0 (Macintosh; ..)
- Response headers: 응답 정보
    - ex. Server: apache
- Entity headers: Entity body 정보
    - ex. Content-type: text/html, Content-Length:3423

### RFC2730

- 과거 Enitity라고 했던 것을 현재 Representation이라고 한다.
    - Request / Response에서 전달할 실제 데이터이다.
- message body를 통해 Representation data를 전달한다.
    - message body에 담긴 data를 payload라고도 한다.
- Representation header는 Representation data를 해석할 수 있는 정보를 제공한다.
    - data type(html, json) / length, 압축 정보 등

### Representation headers

- Content-Type: 데이터의 형식
    - 미디어 타입, 문자 인코딩
        - ex. text/html: charset=utf-8
        - application/json
        - image/png
- Content-Encoding: 데이터의 압축 방식
    - 데이터를 전달하는 곳에서 압축 후 headers에 정보를 추가하고, 받는 쪽에서 headers의 정보를 가지고 압축 해제
        - ex. gzip, deflate, identity
- Content-Language: 데이터의 자연 언어
    - ex. ko, en, en-US
- Content-Length 데이터의 길이
    - byte 단위
    - Transfer-Encoding을 사용하면 Content-Length를 사용하면 안된다.

<br>

Reference: https://www.inflearn.com/course/http-%EC%9B%B9-%EB%84%A4%ED%8A%B8%EC%9B%8C%ED%81%AC/
