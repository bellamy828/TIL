# TCP vs UDP

## What is TCP/IP and UDP?

### TCP/IP

- 인터넷에서 사용하는 프로토콜 그룹
- Application - Transport - Network - Data link - Physical, 총 5계층으로 나뉜다.
    - Transport layer
        - 두 응용 계층 사이에서의 process to process 통신을 제공한다.
            - prcoess는 응용 계층에서 구동중인 프로그램이며, 각각의 prcoess는 자신의 port number를 갖는다.
        - 응용 계층으로부터  메시지를 받아 전송 계층 [패킷](https://ko.wikipedia.org/wiki/%EB%84%A4%ED%8A%B8%EC%9B%8C%ED%81%AC_%ED%8C%A8%ED%82%B7)으로 캡슐화하여 전송한다.(Segment, Datagram)
        - 전송계층의 주된 프로토콜은 TCP, UDP이다.
            - TCP(Transmission Control Protocol): 연결형, 신뢰성 전송 프로토콜, TCP로 전송하는 패킷을 Segment라고 한다.
            - UDP(User Datagram Protocol): 비연결형, 비신뢰성 전송 프로토콜, UDP로 전송하는 패킷을 Datagram이라고 한다.

### TCP(Transmission Control Protocol)

- 연결형, 신뢰성 전송 프로토콜
    - ex. 매우 큰 문서파일을 다운로드한다면 신뢰성이 보장되어야 할 것이다. 문서의 일부분이 손실되거나 훼손되지 않고 원본이 보장되는 것이 중요하고, 신뢰성을 보장하기 위해 지연되는 것은 상대적으로 중요한 문제가 아니다.
- 데이터를 전송하기 전에, 두 호스트의 전송 계층 사이에 논리적 연결을 설립, 그후 데이터를 전송하고 완료되면 해제한다(connection setup → data transfer → connection termination)
- TCP가 전체 스트림을 순서에 맞게, 오류 없이, 부분적인 손실이나 중복 없이 전송하는 것을 보장하여 신뢰성 있는 서비스를 제공한다.
    - 흐름제어: 데이터를 보내는 속도와 데이터를 받는 속도의 밸런스를 맞추는 것
    - 오류제어: 훼손, 손실, 순서가 맞지 않거나 중복된 Segment를 감지하고 재전송하거나 폐기한다.
        - TCP header의 checksum, 확인응답, 타임-아웃등을 통해 수행된다.

### UDP(User Datagram Protocol)

- 비연결형, 비신뢰성 전송 프로토콜
    - 실시간 상호작용이 필요한 live 방송에서는 음성과 영상을 한 프레임 씩 전송한다. 이 때 전송 계층에서 훼손되거나 손실된 프레임을 재전송한다면 지연이 발생한다. 패킷이 손실되어 짧은 시간 영상에 문제가 생기더라도 시청에 큰 무리는 없을 것이기 때문에 UDP를 사용한다.
- 작은 메시지를 보내거나 신뢰성을 크게 고려하지 않아도 되는 상황에서 사용한다.
- 논리적 연결을 설립하지 않고 Datagram을 전송한다.
- 또한 흐름제어, 오류제어, 혼잡제어를 제공하지 않아, 오버헤드가 적고 가볍다.

  
  <br>
  
  Reference: https://www.nossi.dev/interview/cs/network#64afa397-031b-4c7e-a844-c988a6c66de3
