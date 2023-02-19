# OSI 7 Layers & TCP/IP 4 Layers

## What is OSI 7 Layers and TCP/IP 4 Layers?

### OSI 7 Layers and TCP/IP 4 Layers

- 각 계층은 하위 계층의 기능을 이용하고, 상위 계층에게 기능을 제공한다.
    - ex. HTTP 프로토콜은 TCP 프로토콜과 IP 프로토콜을 이용해서 작동한다.
- 일반적으로 상위 계층의 프로토콜은 소프트웨어, 하위 계층의 프로토콜은 하드웨어로 구현된다.
    - ex. 물리 계층의 통신은 케이블을 통한 전기 신호로 이루어진다.

### Encapsulation & Decapsulation

- Encapsulation: 통신 프로토콜의 특성을 포함한 정보를 Header에 포함시켜서 하위 계층에 전송하는 것을 말하며, 최종적으로 물리 계층에서 binary 데이터로 변환되어 전송된다.
- Decapsulation: 통신 상대측에서 이러한 Header를 역순으로 제거하면서 상위 계층으로 Data를 전달, 최종적으로 원본 Data를 얻는 과정을 역캡슐화라고 한다.
- 사용자는 최상위 계층인 응용 계층에서 인터넷 접속(HTTP), 메일 전송(SMTP), 파일 전송(FTP), 원격 로그인(Telnet) 등의 작업을 수행한다.

  
  <br>
  
Reference: https://www.nossi.dev/interview/cs/network#64afa397-031b-4c7e-a844-c988a6c66de3
