## IP(Internet Protocol)

인터넷 통신을 위한 규칙, IP Address를 기반으로 상호 통신할 수 있다.

### 역할

- 지정한 IP Addressd에 데이터 전달
- Packet이라는 통신 단위로 데이터 전달

### 한계

- 비연결성: Packet을 받을 대상이 없거나 서비스 불능 상태여도 Packet을 전송한다.
- 비신뢰성 : 중간에 Packet이 사라지거나, Packet을 여러번 보냈을 때 순서대로 전송되지 않을 수도 있다.
- 같은 IP를 사용하는 서버에서 통신하는 애플리케이션이 2개 이상일 경우, 구분할 수 없다
- 전송 대상(e.g.Sever)가 서비스 불능 상태여도 Client는 알 지 못한 채로  Packet을 전송할 수도 있다.

<br>

reference: https://www.inflearn.com/course/http-%EC%9B%B9-%EB%84%A4%ED%8A%B8%EC%9B%8C%ED%81%AC#reviews
