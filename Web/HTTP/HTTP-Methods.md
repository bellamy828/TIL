# 4. HTTP Methods

## Restful API 설계

### URI 설계

- URI는 Resource만 식별해야 한다.
    - ex. ‘Members’ O / ‘Members를 등록한다’ X
        - 회원이라는 리소스만 식별하면 된다.
        - 회원 리소스를 URI에 매핑한다.
        - URI 구체적인 값은 계층 구조상 상위를 컬렉션으로 보고 복수 단어를 사용하는 것이 좋다.
- 해당 Resoucef를 대상ㅇ으로 하는 행위는 HTTP Method를 사용하여 구분한다.

## HTTP methods

### 주요 methods

- GET: 리소스를 조회한다.
    - Server에 전달하고 싶은 데이터는 query를 통해서 전달한다.
    - Message body를 사용해서 데이터를 전달할 수는 있지만, 실무에서는 지원하지 않는 Server가 많기 때문에 권장하지 않는다.
- POST: 주로 데이터를 등록할 때, 변경된 프로세스 처리에 사용한다.
    - Message body를 통해 Server로 요청 데이터를 전달한다.
        - Message body를 통해 들어온 데이터를 처리하는 모든 기능을 수행한다.
    - 대상 리소스가 리소스의 고유한 의미 체계에 따라 요청에 포함된 표현을 처리하도록 요청한다.(공식 문서 Spec)
        - HTML FORM에 입력한 정보로 회원 가입, 주문
        - 게시판 글쓰기, 댓글 달기
        - 신규 주문 생성
        - 문서 끝에 내용 추가하기등
        - 각 리소스마다 POST 요청을 어떻게 처리할 것긴지 따로 정해야한다.
- PUT: 리소스를 대체, 해당 리소스가 없으면 생성한다.
- PATCH: 리소스 부분 변경한다.
- DELETE: 리소스를 삭제한다.

### 기타 methods

- Head: GET과 동일하지만 메시지 부분을 제외하고, 상태 줄과 헤더만 반환한다.
- OPTIONS: 대상 리소스에 대한 통신 가능 옵션(메서드)를 설명한다.(주로 CORS에서 사용)
- CONNECT: 대상 자원으로 식별되는 서버에 대한 터널을 설정한다.
- TRACE: 대상 리소스에 대한 경로를 따라 메시지 루프백 테스트를 수행한다.

<br>

Reference: https://www.inflearn.com/course/lecture?courseSlug=http-%EC%9B%B9-%EB%84%A4%ED%8A%B8%EC%9B%8C%ED%81%AC
