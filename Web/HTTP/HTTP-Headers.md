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

### **Content negotiation**

- Client가 Server에게 응답 받을 표현에 대해서 협상하는 것으로 Request에서만 사용한다.
- Accept: Client가 선호하는 Media type
    - 구체적인 것이 우선이다.
        
        > GET /event<br>
        Accept-Language: ko-KR,ko;q=0.9,en-US;q=0.8,en;q=0.7
        > 
        1. text/plain;format-flowed
        2. text/plain
        3. text/*
        4. */*
    - 구체적인 값 끼리 다시 우선순위를 부여한다.
        
        
        | Media type | quality |
        | --- | --- |
        | text/html;level=1 | 1 |
        | text/html | 0.7 |
        | text/plain | 0.3 |
        | image/jpeg | 0.5 |
        | text/html;level=2 | 0.4 |
        | text/html;level=3 | 0.7 |
- Accept-Charset: Client가 선호하는 문자 인코딩
- Accept-Encoding: Client가 선호하는 압축 인코딩
- Accept-Language: Clinet가 선호하는 자연 언어
    - Quality Values(q)를 사용한다.
    - 0~1, 클수록 높은 우선순위
    - 1은 생략한다.
        
        > GET /event<br>
        Accept-Language: ko-KR,ko;q=0.9,en-US;q=0.8,en;q=0.7
        > 
        1. ko-KR;q=1(q 생략)
        2. ko;q=0.9
        3. en-US;q=0.8
        4. en;q=0.7

### Transfer-Encoding

- 단순 전송
    - Content-Length만 기입하여 요청하고 응답 받는다.
- 압축 전송
    - Content-Length와 Content-Encoding 정보를 기입하여 요청하여 압축된 표현을 응답받는다.
- 분할 전송
    - Transfer-Encoding: Chunked를 기입하여 분할된 응답 표현을 받는다. 분할되어 오기 때문에 Content-Length는 기입하지 않는다.
- 범위 전송
    - Range: bytes=1001-2000(in Request headers)와 같이 기입하여 보내면, Server에서 응답 header에 Content-Range: bytes 1001-2000 / 2000과 같이 범위를 표시하여 보내준다.

### 일반 정보

- From
    - 유저 에이전트의 email 정보
    - 일밙적으로 잘 사용되지 않으며, 검색 엔진 같은 곳에서 주로 사용, Request에서 사용된다.
- Referer
    - 현재 요청한 페이지의 이전 웹 페이지 주소를 가리키며 Request에서 사용된다.
    - A → B로 이동하는 경우 B를 요청할 때 Referer: A를 포함해서 요청한다.
    - Referer를 사용해서 유입 경로 분석 가능하다.
    - referrer가 잘못 표기된 단어이지만, 이미 이 단어를 토대로 header가 만들어지고 널리 쓰여서 다시 수정하지 못하고 사용한다.
- User-Agent
    - Client의 Application 정보(Web browser 정보 등), Request에서 사용된다.
    - 통계 정보
    - 어떤 종류의 Browser에서 장애가 발생하는지 파악 가능
- Server
    - Proxy Server가 아닌 요청을 처리하는 Origin server의 소프트웨어 정보, Response에서 사용된다.
        - ex. Server: Apache/2.2.22(Debian)
- Date
    - Response message를 전송한 날짜와 시갼을 표기한다.
    - 과거에는 Request에서도 표기했지만 최신 스펙에서는 Response에서만 사용한다.

### 특별한 정보

- Host
    - Request header이며, 하나의 Server가 여러개의 Domain을 가진 경우, Host 정보가 없는 Request를 처리할 수가 없다.
    - 따라서 필수 정보이다.
- Location
    - Web browser는 3xx 응답 결과의 Location header에 기재된 주소로 Redirect
    - cf. 201 (created)의 Location은 요청에 의해 생성된 Resourece URI
- Allow
    - 허용 가능한 HTTP Methods 표기
    - 405 Method Not Allowed Response header에 포함해야 한다.
- Retry-After
    - 503 Service Unavailable Response에서 유저 에이전트가 다음 요청을 하기까지 기다려야 하는 시간을 표기할 수 있도록 하는 헤더
        - 날짜 표기와 초단위 표기가 가능하다.

### Authorization

- Client 인증 정보를 Server에 전달한다.

### WWW-Authenticate

- 401 Unauthorized Response에 표기하며, Resource에 접근할 때 필요한 인증 방법을 정의해준다.

<br>

Reference: https://www.inflearn.com/course/http-%EC%9B%B9-%EB%84%A4%ED%8A%B8%EC%9B%8C%ED%81%AC/
