# [Cache](https://ko.wikipedia.org/wiki/%EC%BA%90%EC%8B%9C)

웹에서 한 번 접근했던 데이터를 다시 다운로드 받지 않고 빠르게 접근할 수 있도록 데이터나 값을 미리 복사해놓는 임시 저장소


## 필요성

### 캐시가 없을 때
- 데이터가 변경되지 않아도 계속 네트워크를 통해서 데이터를 다운로드해야 한다.
- Browser 로딩 속도가 저하된다.
### 캐시 적용
- 캐시 유효 시간 동안 네트워크를 사용하지 않아도 된다.
- Browser 로딩 속도가 빨라진다.
### 캐시 시간 초과
- Server를 통해 데이터를 다시 조회하고 캐시를 갱신한다.
    - 이때 다시 네트워크 다운로드를 진행한다.
        - 하지만 데이터가 바뀌지 않았다면, 유효시간 이후 다운로드는 다시 자원 낭비이고 이를 해결하기 위해서 검증 header와 조건부 요청을 한다.

## 검증 헤더
Client Browser Cache에 저장된 데이터가 Server의 데이터와 같은지 확인해야 한다.

### Last-Modified
- 검증 과정
    1. Server Response Headers에 Last-Modified: 날짜를 기재하여 보내준다.
    2. 이후 Client 캐시 사용 시간이 만료되면 Request headers에 if-modified-since: 날짜를 기재하여 전송한다.
    3. Server가 해당 요청 검증 헤더를 확인하여 데이터 수정된 내용이 없다면 304 Not Modifed로 전송, Header에 필요한 데이터만 담고 **Body를 비워서 응답한다**. 
        - 만약 Server의 Last-Modified 값이 갱신 됐다면 200 OK, 모든데이터를 전송한다.
    4. 304 code 응답을 확인한 Browser가 Cache에 저장된 데이터가 같다는 것을 확인하고, 캐시의 메타 데이터를 갱신하여 저장되어 있는 캐시를 재활용한다.
- 단점
    - 1초 미만, ms 단위로 캐시 조정 불가하다.
    - Date 기반의 로직을 사용한다.
        - 실질적인 수정이 이루어지지 않더라도 로그가 남아서 마지막 수정일이 변경된 경우 의도치 않게 변경 없는 데이터를 다시 전송하게 될 수도 있다.

### Etag(Entity Tag)
Etag header의 값이 같으면 cache를 유지/재활용, 다르면 다시 다운로드 한다.

- 검증 방법
  - 캐시용 데이터에 임의의 고유한 버전을 부여하는 방법
      - ex. ETag: “v1.0”, ETag: “a2fjjfqkjfkj3”
  - Hash를 활용하여 데이터가 실질적인 데이터가 변경되었을 때 해시값이 달라지도록 하는 방법
- 검증 과정
  1. Cache에 저장된 데이터의 eTag 정보를 확인하여 Request headers에 if-None-Match에 Etag 값을 기재하여 요청한다. 
  2. Sever가 if-None-Match 값을 확인하여 Server의 ETag와 같으면 304 Not Modified, body를 비워서 응답한다.
     - Server의 ETag 값과 다르면 200 OK, 모든 데이터를 body에 담아 전송한다.
- 장점
    - Client는 단순히 ETag 값을 Server에 전송하기만 하면 되고, Server는 Cache 제어 로직을 온전히 관리할 수 있다.
- 캐시 제어 헤더
  - Cache-Control
    - max-age: 캐시 유효 시간(초)
    - no-cache: 데이터는 캐시할 수 있지만, 항상 Origin server에 검증하고 사용한다.
    - no-store: 보안이 중요한 데이터이기 때문에 저장하면 안된다.
  - Pragma
    - HTTP 1.0 하위 호환으로 현재는 사용하지 않는다.
  - Expires
    - 캐시 만료일을 정확한 날짜로 지정한다.
    - HTTP 1.0 부터 사용한다.
    - 더 유연한 하게 시간을 조정할 수 있는 Cache-Control: max-age 사용을 권장한다.
        - 혼용시 Expires는 무시한다.

### [Proxy](https://ko.wikipedia.org/wiki/%ED%94%84%EB%A1%9D%EC%8B%9C_%EC%84%9C%EB%B2%84)

Origin Server와 물리적으로 먼 곳에 위치한 Client 권역에 구축한 Server로 특정 국가, 지역에 좀 더 빠른 접근이 가능하게 한다.

- Cache-Control: public
    - 응답이 public cache에 저장되어도 된다.
- Cache-Control: private
    - 해당 사용자만을 위한 응답, private 캐시에 저장하는 것이 기본값
- Cache-Control: s-maxage
    - Proxy Cache에만 적용되는 max-age
- Age:60
    - Origin Server에서 응답 후 Proxy caceh 내에 머문 시간(초)

### 캐시 무효화

- Cache-Control: no-cache
  - 데이터는 캐시해도 되지만, 항상 Origin Sever에 검증하고 사용한다.
- Cache-Control: no-store
  - 데이터에 민감한 정보가 있으므로 저장하면 안된다.
- Cache-Control: must-revalidate
  - 캐시 유효시간이 있다면 캐시를 사용한다. 
  - 캐시 만료 이후 최초로 조회할 때 Origin Sever에 검증해야 한다.
  - Origin Server에 접근할 수 없을 때 반드시 오류가 발생해야 한다.(504 Gateway Timeout)

- Pragama: no-cache
  - HTTP 1.0 하위 호환

<br>

Reference: https://www.inflearn.com/course/http-%EC%9B%B9-%EB%84%A4%ED%8A%B8%EC%9B%8C%ED%81%AC#
