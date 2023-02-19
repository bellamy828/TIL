# TCP 3(4) way handshake

## What is TCP 3(4) way handshake?

### TCP Data Transfer Process

1. Connection setup(TCP 연결 초기화) 
    - 3 way handshaking
2. Data tansfer
3. Connection termniation 
    - 4 way handshaking

### TCP Flags

- 패킷의 Flag 값에 따라 세션 연결과 종료 데이터 전송등 기능이 달라진다.
    - SYN(Synchronization)
        - 연결 요청 플래그
        - TCP에서 세션을 성립할 때 가장 먼저 보내는 패킷
        - 시퀀스 번호를 임의적으로 설정하여 세션을 연결할 때 사용, 초기에 시퀀스 번호를 전송한다.
    - ACK(Acknowledgement)
        - 응답 플래그
        - 상대방으로부터 패킷을 받았다는 것을 알리는 패킷(다른 플래그와 같이 출력될 수도 있음)
        - ACK 응답을 통해 보낸 패킷에 대한 성공/실패를 판단하여 재전송하거나 다음 패킷을 전송한다.
    - FIN(finish)
        - 연결 종료 요청
        - 더이상 전송할 데이터가 없음을 나타낸다.
    - 그밖에도 RST(Rest), PSH(Push), URG(Urgent), Placeholder 등이 있다.

### 3 way handshake process

- TCP 연결 초기화: TCP/IP 프로토콜로 통신하기 전에 정확한 정보 전송을 위해 상대방 컴퓨터와 세션을 수립하는 과정이다.
    1. Client → Server, SYN 패킷 전송
    2. Server → Client, SYN + ACK 패킷 전송
    3. Clinet → Sever, ACK 패킷 전송 
    4. 이후 데이터 통신이 가능해진다.

### 4 way handshake

- TCP Connection termination을 위해서 4 way handshaking이 필요하다.
- 양방향으로 2개의 연결이 독립적으로 닫히기 때문에 4way 단계가 필요하다.
    1. Clinet processs에서 active close를 하면, Client TCP에서 FIN Segment를 보낸다.
    2. Server는 FIN Segment를 받았다는 응답에 대한 ACK를 Client에게 보낸다. 이때 server의 Process에 [EOF](https://ko.wikipedia.org/wiki/%ED%8C%8C%EC%9D%BC_%EB%81%9D)를 보내지만, 아직 process는 close되지 않을 수 있다.
    3. Server process로 Passive close를 받으면 server tcp에서 FIN Segment를 Client TCP에게 보낸다.
    4. Server TCP가 ACK를 받으면 연결이 종료된다.
    
<br>

Reference

- [https://skstp35.tistory.com/250](https://skstp35.tistory.com/250)
- [https://www.nossi.dev/interview/cs/network#64afa397-031b-4c7e-a844-c988a6c66de3](https://www.nossi.dev/interview/cs/network#64afa397-031b-4c7e-a844-c988a6c66de3)
