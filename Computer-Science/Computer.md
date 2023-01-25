# 컴퓨터 구조와 원리

## 트랜지스터

![image](https://user-images.githubusercontent.com/72433598/211841196-1a4985f3-9316-4e05-a01a-ed939c3ea5fa.png)

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
    - (논리소자)를 가지고 계산기를 만들 수 있다.
        - 1bit 가산기(ADD)
            - 2개의 트랜지스터를 가지고 입력이 서로 같을 때 0, 다를 때 1을 출력하는 XOR(S; 합의 결과) / 입력이 모두 1일 때 1을 출력하는 AND(C;올림수)
            - 그렇다면 2bit 가산기도 마찬가지로 1bit 가산 결과인 C를 가지고 3번 째 입력으로 넣고 결과가 나옴
        - 마찬가지로 뺄셈, 곱셈, 나눗셈도 논리소자를 가지고 만들어 낼 수 있게 된다.

## 컴퓨터

- 명령을 하나씩 순서대로 수행하는 기계
- 프로그램: 어떤 명령을 어떻게 수행할 것인지 적어놓은 것이라 볼 수 있음
- 최초의 컴퓨터의 형태: 튜링 머신 시작으로 메모리 상에서 작업을 하게 되는 폰 노이만 머신
- 컴퓨터 안에서 논리연산 이외에 문자, 이미지, 사운드를 표현하는 원리
    - 문자
        - ASCII
            - 1byte = 8bit = 2^8 = 256
            - 0~255 까지의 문자 코드를 표현할 수 있음
            - 초기 문자 코드이기 때문에 영문자만 표현 가능
        - Unicode
            - 1~3byte 이나 2byte라고 보면됨
            - 영문자 이외에 다른 문자도 표기 가능
    - 이미지
        - 각각의 픽셀의 색 나열이라고 볼 수 있음
            - 픽셀 하나에 R,G,B가 묵여있음
        - 색을 숫자로 표현해야했음
            - RGB, 빛의 3원소를 표현하면 모든 색을 표현할 수 있음
            - RGB 각각 0-255 까지의 채도?를 표현하고 모두 255일 때 화이트, 모두 0일 때 블랙
            - RGB 각각 1byte 씩 하나의 색은 총 3 byte로 표현 가능 + 투명도 까지 추가하면 4byte
- 하드웨어 동작 원리(요리에 비유)
    - 요리사(동작의 주체) → 요리사
    - 레시피(책) → 프로그램
        - 무엇을 어떻게 할 것인지 적혀있음
    - HDD → 마트
        - 다양한 요리 재료가 있지만 먼 곳
        - BUS를 타고 가야함 → 하드웨어를 연결하는 전선 다발도 BUS라고 함
    - RAM → 냉장고
    - CACHE → 필요한 요리재료 묶음(밀키트)
        - RAM에서 당장 연산에 필요한 Chunk 가져옴
        - 대략 4kb의 용량
    - REGISTER → 도마
        - 실제 연산에 들어가기 전 준비시켜 놓는 자리
        
        ex) ADD(A, B) 당장 A와 B를 연산하기 전에 A와 B를 준비시켜놓는 곳?
        
        - 연산 결과가 CACHE나 MEMORY에 저장됨

## 프로그램

- 명령과 순서를 쓴 문서
- 컴퓨터 입장에서는 기계어(0, 1)를 실행하는 것

## 프로그래밍 언어

- 프로그램을 작성한 언어
- 정적 언어(컴파일 언어)
    - C, C++, Go
    - 코딩 → 빌드 → 기계어
        - 빌드: 프로그래머가 작성한 문서를 컴파일러가 기계어로 변환하는 과정(역변환 불가)
    - 실행하기 전에 미리 기계어로 모두 변환시켜놓고 실행
    - 실행 속도가 상대적으로 빠름
- 동적 언어
    - JAVA, C#, Python
    - 실행 속도가 상대적으로 느림
        - 초창기에는 확실히 정적 언어보다 실행 속도가 느렸으나, 현재는 드라마틱한 차이는 없음
        - 또한 라이브러리나 인프라등 생산성 면에서의 이점이 있기 때문에 JAVA 같은 동적 언어가 개발에 더 용이한 부분도 있음
    - 완전히 기계어로 변환시켜 놓는게 아닌 중간 단계?가 있음
- 정적 언어의 실행 속도가 빠름에도 불구하고 동적 언어가 생긴 이유 → 대중 OS 별로 다른 변환이 필요했음
    - 결국 각기 다른 OS 뿐만 아니라 MS 같은 경우는 각 칩셋(CPU) 별로도 컴파일러가 다른 결과물을 내야함
    
    ex) 인텔, IBM등 칩셋 제조 회사 별로 OP 코드가 다름 → 가령 ADD 연산 코드가 인텔은 0001, IBM은 0111
    
    - 칩셋, OS 관계없이 소스 코드를 필요할 때 마다 변환하여 실행하기 위해서 고안됨
- 어셈블리어
    - 기계어와 고수준 언어 사이의 저급 언어
    - 컴파일 된 언어에서 다시 역변환이 가능
    - 인간의 입장에서는 기계어 보다 나은 가독성, 작성된 언어를 받아들이는 컴퓨터 입장에서 가볍고 실행 속도가 빠르다는 이점
    - 하지만 인간 입장에서는 자연어 보다는 생산성이 떨어질 수 밖에 없음
  
    <br>
    
  Reference(https://www.youtube.com/@TuckerProgramming)