# Status code

클라이언트가 보낸 요청에 대한 응답을 숫자 코드로 분류하여 상태를 알린다.

## 1xx: Informational

요청을 받고 처리중

<br>

## 2xx: Successful

요청 정상 처리 완료

### 200 OK

- GET 요청에 대한 성공 응답

### 201 Created

- POST 요청에 대한 성공 응답

### 202 Accepted

- 요청이 접수되었지만 처리가 완료되지 않은 상태
    - ex. 요청 접수 후 1시간 뒤에 [Batch process](https://ko.wikipedia.org/wiki/%EC%9D%BC%EA%B4%84_%EC%B2%98%EB%A6%AC)가 요청을 처리함

### 204 No Content

- 서버가 요청 내용을 성공적으로 수행했지만, Response payload에 전송할 데이터가 없는 상태
    - ex. 웹 문서 편집기의 save 기능
        - save 버튼 누른 후 확인할 내용이 없고, 같은 화면을 유지한다.
        - 이 때 응답 코드 204만으로 요청 성공을 인식할 수 있다.

<br>

## 3xx: Redirection

요청 내용을 완료하기 위해 Client(Browser)에서 추가 작업이 필요한 상태

### Redirection

- Web browser는 3xx 응답의 결과에 Location Header가 있으면 해당 Location으로 이동한다.
    - 영구 리다이렉션: 특정 리소스의 URI가 영구적으로 바뀜
        - ex. /members → /users
    - 일시 리다이렉션: 일시적인 변경
        - ex. 주문 완료 후 주문 내역 화면으로 이동
        - PRG: Post / Redirect / Get
            - ex. POST로 주문 후에 Web browser를 새로고침하면 다시 요청하여 중복주문이 될 수 있다.
                - → POST로 주문 후에 결과 화면을 GET method로 redirect, 새로 고침해도 결과화면을 GET으로 조회한다.
                    - Client 입장에서도 편리하고, Server 입장에서도 오류를 줄일 수 있다.
    - 특수 리다이렉션
        - 결과 대신 캐시를 사용

### 301 Moved Permanently

- Redirect 하면서 요청 method가 GET으로 바뀌고, 본문이 제거될 수도 있다.
- 실무에서는 GET 요청으로 전환해서 처리하는 경우가 많다.

### 308 Permanent Redirect

- 301과 기능은 같다.
- Redirect 해도  원래 요청했던 method를 사용하고 body를 유지한다.
- 실무에서는 301의 경우 처럼 GET 요청으로 전환하여 다시 POST 요청을 하도록 한다.

### 302 Found

- 본래 302 스펙 정의 목적은 HTTP Method를 유지하는 것이었으나, Web browsers가 대부분 GET으로 동작도록 했다.
    - 그래서 더 명확한 목적을 갖는 303, 307도 정의하게 되었다.
        - 303, 307 사용을 권장하지만 현실적으로 많은 애플리케이션 라이브러리가 302를 기본값으로 사용한다.
    - 301 대응으로 308도 정의하게 되었다.
- Redirect 할 때 Request method가 GET으로 바뀌고 분문이 제거될 수도 있다.
- PRG 구현에 사용한다.

### 307 Temporary Redirect

- 302와 기능은 같다.
- Redirect 할 때, 원래 Request method를 그대로 사용하고 Message body를 유지한다.

### 303 See other

- 302와 기능은 같다.
- Redirect 할 때, Request method가 GET으로 변경한다.

### 304 Not Modified

- Client에게 Resource가 수정되지 않았다고 알려주고, Local PC에 저장된 Cache를 재사용하도록 한다.(Cache로 Redirect)
- Local Cache를 사용하도록 해야하므로 Response Message Body를 포함하면 안된다.
- 조건부 GET, HEAD 요청할 때에 사용한다.

<br>

## 4xx: Client Error

Client의 잘못된 요청, 문법 등으로 Server가 요청을 수행할 수 없는 상태이며, 재시도 또한 분명 실패한다.

### 400 Bad Request

- Client 잘못으로 요청 Parameter, API 스펙이 맞지 않는 상태이다.

### 401 Unauthorized

- Authentication(인증)이 되지 않은 상태로, 응답에 WWW-Authenticate header와 함께 인증 방법을 설명해야 한다.
- Authentication vs Authorization
    - Authentication: Client가 누구인지 확인, 로그인
    - Authorization: 권한 부여, 로그인 하여 누구인지 확인하고, 접근 권한등의 인가

### 403 Forbidden

- 주로 인증 자격 증명은 있지만, 접근 권한이 불충분한 경우
    - ex. admin 등급이 아닌 사용자가 로그인은 했지만, Admin 등급의 resource에 접근하는 경우

### 404 Not found

- 접근하고자 하는 Resource가 Server에 없는 상태
- 또는 Client가 권한이 부족한 Resource에 접근, 해당 Resource를 숨기고 싶을 때

<br>

## 5xx: Server Error

Server에 문제가 있기 때문에 재요청 후에는 성공할 수 도 있다.

### 500 Internal Server Error

- 서버 내부 문제로 오류가 발생했을 때, 애매한 상황에 많이 사용되는 코드이다.
- 로직에 문제가 생기거나 쿼리, DB 문제등의 기술적인 문제에 사용해야한다.
- 미성년자 접근 권한이나 그외 상식적으로 잘못된 요청에 대한 응답으로 사용하면 안된다.

### 503 Service Unavailable

- Server의 일시적인 과부하 또는 예정된 작업으로 잠시 요청을 처리할 수 없는 상태
- Retry-After header-field로 얼마나 걸리는지 보낼 수도 있다.

<br>

Reference: https://www.inflearn.com/course/lecture?courseSlug=http-%EC%9B%B9-%EB%84%A4%ED%8A%B8%EC%9B%8C%ED%81%AC
