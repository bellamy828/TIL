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

<br>

Reference: https://www.inflearn.com/course/http-%EC%9B%B9-%EB%84%A4%ED%8A%B8%EC%9B%8C%ED%81%AC#
