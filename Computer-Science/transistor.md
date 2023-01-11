# 컴퓨터 구조와 원리

## 트랜지스터

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/1b640a92-3cb8-4825-8102-e9b1a9662234/Untitled.png)

- 컴퓨터를 구성하는 가장 기본적인 요소(생물의 근본이 C;탄소인 것 처럼)
- CPU는 트랜지스터 덩어리
- 컴퓨터에서는 주로 신호 on/off 스위치 역할로 이해
    - 반도체
        - 입력이 있어 base에 전압을 걸면 전기가 흐를 수 있는 전도체가 되고
        - 그렇지 않으면 부도체가 되어 전류가 흐를 수 없음
        
        ex) AND gate → 2개의 트랜지스터가 모두 입력신호가 있어야만 출력이 있게됨
        
    - 트랜지스터가 물리적인 스위치와 다른점은 전기적 신호로 제어한다는 점
    - 1과 0을 나타내는 2진법으로 표현(bit) → 트랜지스터 1개라고 볼 수 있음
    - 1byte = 8bit, 1kb = 1024byte, 1mb = 1024kb
    - 1gb = 약 86억 개 정도의 트랜지스터가 모여있는 것
- 논리소자를 만들 수 있다
    - bool 대수: 참/거짓 입력에 따라 출력이 달라짐
        - AND
            - input: true, false → output: false
            - input: false, true→ output: false
            - input: true, true→ output: true
        - OR
            - input: true, false → output: true
            - input: false, true→ output: true
            - input: true, true→ output: true
        - NOT
            - input: 0 → output: 1
            - input: 1 → output: 0
    - 1bit 가산기(ADD)
        - 2개의 트랜지스터를 가지고 입력이 서로 같을 때 0, 다를 때 1을 출력하는 XOR(S; 합의 결과) / 입력이 모두 1일 때 1을 출력하는 AND(C;올림수)
        - 그렇다면 2bit 가산기도 마찬가지로
