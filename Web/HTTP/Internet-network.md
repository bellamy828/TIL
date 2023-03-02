## IP(Internet Protocol)

인터넷 통신을 위한 규칙, IP Address를 기반으로 상호 통신할 수 있다.

### 역할

- 지정한 IP Addressd에 데이터 전달
- Packet[^1]이라는 통신 단위로 데이터 전달

### 한계

- 비연결성: Packet을 받을 대상이 없거나 서비스 불능 상태여도 Packet을 전송한다.
- 비신뢰성 : 중간에 Packet이 사라지거나, Packet을 여러번 보냈을 때 순서대로 전송되지 않을 수도 있다.
- 같은 IP를 사용하는 서버에서 통신하는 애플리케이션이 2개 이상일 경우, 구분할 수 없다
- 전송 대상(e.g.Sever)가 서비스 불능 상태여도 Client는 알 지 못한 채로  Packet을 전송할 수도 있다.

## TCP(Tansmission Control Porotocol)

### TCP/IP 4 layers

|  | 실제 프로토콜 |
| --- | --- |
| Application Layer | HTTP, FTP, DNS, Telnet, SMTP, SSH, … |
| Transport Layer | TCP, UDP, … |
| Internet Layer | IP, ICMP, AR, … |
| Network Interface Layer | Ethernet |

### 특징

- IP Packet의 정보(출발 / 목적지 IP)만으로는 한계가 있기 때문에 TCP Segment(출발 / 목적지 Port, 전송 제어, 순서, 검증 정보등)를 보완하여 신뢰성을 보장한다.
- 연결 지향적이다.
    - TCP 3 Way Handshake(가상 연결)
        - 단 논리적으로만 연결된 상태이며, 물리적인 연결은 아니다.
- 데이터 전송 성공 여부를 알 수 있다.
- 데이터 전송 순서를 보장한다.
- 대부분의 Application에서 TCP를 사용한다.

### 3 Way Handshake

1. Client는 Server에게 SYN(접속 요청) Message를 전송한다.
2. 성공적으로 요청을 받은 Server는 Client에게 SYN + ACK(요청 수락) Message를 전송한다.
3. Server의 응답을 성공적으로 받은 Client는 다시 Server에 ACK Message를 전송한다.(최근에는 3번 과정에서 ACK Message와 동시에 데이터를 전송하도록 최적화되었다.)

## UDP(User Datagram Protocol)

### 특징

- 데이터 전송 여부 및 순서가 보장되지 않지만 가볍고 빠르다.
- IP와 거의 같지만 Port, [Checksum](https://ko.wikipedia.org/wiki/%EC%B2%B4%ED%81%AC%EC%84%AC) 기능을 추가한 형태로 볼 수 있다.
- Application에서 추가적으로 최적화가 가능하다.
    - 기존에 신뢰성 있지만 다소 무거운 TCP 기반의 인터넷 통신에 비해, 더 가볍고 효율적으로 최적화가 가능해 최근 HTTP/3 기반 개발에서 각광 받고 있다.

## Port

### 필요성

- 만약 Client가 2개 이상의 HTTP 통신 작업을 한다면 각각의 응답이 어느 서버에서 왔는지, 어떤 프로세스에 해당하는지 구분해야 하는데, IP만 가지고는 구분할 수 없다.
- 따라서 TCP Segment에 출발지 Port, 목적지 Port 정보를 담는다.

### Port number

- 0 ~ 65535 까지 할당 가능하다.
- 0 ~ 1023 까지는 잘 알려진 포트로 사용하지 않는 것이 좋다.
    - 20, 21 → [FTP(File Transfer Protocol)](https://ko.wikipedia.org/wiki/%ED%8C%8C%EC%9D%BC_%EC%A0%84%EC%86%A1_%ED%94%84%EB%A1%9C%ED%86%A0%EC%BD%9C)
    - 23 → [TELNET](https://ko.wikipedia.org/wiki/%ED%85%94%EB%84%B7)
    - 80 → HTTP
    - 443 → HTTPS

## [DNS(Domain Name System)](https://ko.wikipedia.org/wiki/%EB%8F%84%EB%A9%94%EC%9D%B8_%EB%84%A4%EC%9E%84_%EC%8B%9C%EC%8A%A4%ED%85%9C)

### 필요성

- IP Address는 기억하기 어렵고, 변경되었을 경우에 원하는 Server로 요청을 보낼 수 없게 된다.

### 개념

- 흔히 전화번호부에 비유한다.
- 사람이 이해하기 쉬운 Domain name을 IP address로 바꾸거나 그 반대의 변환을 한다.
- DNS Server에 Domain을 등록하여 사용할 수 있다.

[^1]:Packet: package + bucket

<br>

reference: https://www.inflearn.com/course/http-%EC%9B%B9-%EB%84%A4%ED%8A%B8%EC%9B%8C%ED%81%AC#reviews
