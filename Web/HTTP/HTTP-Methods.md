# 4. HTTP Methods

## Restful API 설계

### URI 설계

- URI는 Resource만 식별해야 한다.
    - ex. ‘Members’ O / ‘Members를 등록한다’ X
        - 회원이라는 리소스만 식별하면 된다.
        - 회원 리소스를 URI에 매핑한다.
        - URI 구체적인 값은 계층 구조상 상위를 컬렉션으로 보고 복수 단어를 사용하는 것이 좋다.
- 해당 Resoucef를 대상으로 하는 행위는 HTTP Method를 사용하여 구분한다.
    - 단 실무에서 모든 경우를 리소소로만 구분하기엔 어려운 상황이 있다
        - ex. POST  /orders/{orderId}/start-delivery(컨트롤 URI)

## HTTP methods

### 주요 methods

- GET: 리소스를 조회한다.
    - Server에 전달하고 싶은 데이터는 query를 통해서 전달한다.
    - Message body를 사용해서 데이터를 전달할 수는 있지만, 실무에서는 지원하지 않는 Server가 많기 때문에 권장하지 않는다.
- POST: 주로 데이터를 등록할 때, 변경된 프로세스 처리에 사용한다.
    - Message body를 통해 Server로 요청 데이터를 전달한다.
    - 단순히 데이터 생성 / 변경이 아닌 프로세스를 처리할 때에도 사용한다.
        - ex. 배달 주문 프로세스 중 결제 완료 → 배달중 → 배달 완료(프로세스 상태 변경)
        - 위의 예시의 경우 POST의 결과로 새로운 리소스가 생성되지 않는 상황이다.
    - 대상 리소스가 리소스의 고유한 의미 체계에 따라 요청에 포함된 표현을 처리하도록 요청한다.(공식 문서 Spec)
        - HTML FORM에 입력한 정보로 회원 가입, 주문
        - 게시판 글쓰기, 댓글 달기
        - 신규 주문 생성
        - 문서 끝에 내용 추가하기등
        - 각 리소스마다 POST 요청을 어떻게 처리할 것긴지 따로 정해야한다.
    - 다른 method로 처리하기 애매한 경우에도 사용한다.
        - ex. 조회할 데이터를 JSON으로 전송해야 하는데 대부분의 Server는 GET 요청에 Body message에 응답하지 않는 경우가 많으므로 POST로 요청한다.
- PUT: 해당 리소스가 있으면 완전히 대체, 해당 리소스가 없으면 생성한다.
    - Client가 리소스를 정확히 식별해야한다.
        - POST 요청과 다르게 리소스의 정확한 URI를 지정한다.
    - 기존 리소스를 완전히 대체하기 때문에 일부만 수정하는 것은 안되고 PATCH를 사용해야 한다.
- PATCH: 리소스 부분 변경한다.
    - PUT과 다르게 기존 리소스의 일부를 수정할 수 있다.
    - PATCH를 지원하지 않는 Server의 경우 POST를 대안으로 사용하기도 한다.
- DELETE: 리소스를 삭제한다.
    - 보통 요청 Body에 데이터를 담지 않는다.

### 기타 methods

- Head: GET과 동일하지만 메시지 부분을 제외하고, 상태 줄과 헤더만 반환한다.
- OPTIONS: 대상 리소스에 대한 통신 가능 옵션(메서드)를 설명한다.(주로 CORS에서 사용)
- CONNECT: 대상 자원으로 식별되는 서버에 대한 터널을 설정한다.
- TRACE: 대상 리소스에 대한 경로를 따라 메시지 루프백 테스트를 수행한다.

### method의 속성

- 안전성: 요청을 해도 리소스를 변경하지 않는다.
    - GET / HEAD / OPTIONS / TRACE가 해당된다.
    - 단 해당 리소스의 변경 여부만 고려하며, 과도한 트래픽이나 다른 변수에 의한 장애는 고려하지 않는다.
- 멱등성: 한 번의 요청을 하든, 수회의 요청을 하든 결과가 같아야 한다.
    - GET / PUT / DELETE가 해당된다.
    - POST는 멱등성을 갖지 않는다.
        - ex. 주문 프로세스에서 두 번 요청하면 두 번 결제될 수 있다.
    - 자동 복구 메커니즘에 활용된다.
        - 서버가 TIMEOUT 등으로 정상적으로 응답하지 못했을 때, Client가 같은 요청을 해도 되는지 판단하는 근거가 될 수 있다.
    - 외부 요인(3자의 요청)으로 중간에 리소스가 변경되는 것은 고려하지 않고 오직 원 주체의 요청에 대한 결과만 고려한다.
- [캐시](https://ko.wikipedia.org/wiki/%EC%BA%90%EC%8B%9C) 가능 여부
    - GET / HEAD / POST / PATCH는 캐시 가능하다.
        - 실제로는 GET / HEAD 정도만 캐시로 사용한다.
        - POST / PATCH는 본문 내용까지 캐시 키로 고려해야 하므로 구현이 쉽지 않다.

## HTTP Method 활용

### HTTP Request data transfer

- Query parameter를 통한 데이터 전송(GET)
    - 정적 데이터 조회
        - 이미지, 정적 텍스트 문서는 Query parameter 없이 Resource 경로로 단순하게 조회 가능하다.
    - 동적 데이터 조회
        - Query parameter를 사용해서 조회에 필요한 데이터를 전달한다.
        - 주로 검색, 게시판 정렬, 필터 기능에 사용한다.
- Message Body를 통한 데이터 전송(POST / PUT / PATCH)
    - HTML Form 데이터 전송
        - GET / POST methods만 지원한다.
        - 웹 브라우저가 <form> tag의 action(uri)과 method(HTTP Method) attribute를 토대로 HTTP message를 생성 후 전송한다.
            - method를 get으로 설정하면 GET 요청 또한 가능하다.
        - Content-Type
            - `application/x-www-form-urlencode(default)`
                - form의 내용을 message body에 key=value pairs 형태로 담아 전송한다.
                - 전송하는 데이터를 url encoding 처리한다.
                    - ex. abc김 → abc%EA%B9…
            - `multipart/form-data`
                - text 뿐만 아니라 image, audio 등 binary datas를 같이 전송할 때 사용한다.
                    - ex. 파일 업로드

### HTTP API data transfer

- Server to server
    - 백엔드 시스템 통신
- Application Client
    - iOS, Android
- Web Client
    - HTML에서 Form 전송 대신 JS를 통한 통신에 사용(AJAX)
        - ex. React, Vue와 같은 Web client API 통신
- 주요 Methods
    - POST / PUT / PATCH → Messgae Body에 데이터를 담아 전송한다.
    - GET → Query parameter로 데이터를 전송한다.
- Content-Type: application/json을 주로 사용한다.

<br>

Reference: https://www.inflearn.com/course/lecture?courseSlug=http-%EC%9B%B9-%EB%84%A4%ED%8A%B8%EC%9B%8C%ED%81%AC
