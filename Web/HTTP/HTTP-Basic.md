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
- 무상태성, 비연결성
- HTTP Message
- 단순함과 확장 가능

<br>

Reference: https://www.inflearn.com/course/http-%EC%9B%B9-%EB%84%A4%ED%8A%B8%EC%9B%8C%ED%81%AC/
