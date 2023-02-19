# 자료구조와 메모리 구조 이해하기

## 메모리
데이터의 저장 공간

- HDD
    - 소스파일을 저장하는 곳
- RAM
    - 저장된 파일을 실행하면 램 메모리에 데이터가 올라간다
    - 비효율적인 자료구조를 사용하면 프로그램 성능 저하 원인 → 적합한 자료구조를 사용해야함
- 전기 신호를 저장하는 트랜지스터로 이루어져있음
- 전기 신호가 들어오면 1, 전기 신호가 없어지면 0 → 이진수(Bianry Digit) 표현 → bit
- 2진법(Bianry)
    - 0b를 앞에 붙여 표현
    - 1bit는 0과 1 두가지를 표현할 수 있음
    - 1byte == 8bit == 2^8 가지
        - kb, mb, gb 등 메모리가 커지면 표현된 데이터?를 찾기 너무 광범위
        - byte 마다 16진수 address를 달아놓음
- 16진법(Hexadeciaml)
    - 2진수로 표기하기에는 너무 큰 데이터를 표기하기 위해서 사용
    - 0x를 앞에 붙여 표현
    - 6진수 == 2진수 4개
- 메모리 할당
    - int
        - 정수를 표현한 binary digit이 16진수로 표현되어 저장됨
    - Char
        - 컴퓨터는 데이터를 숫자로 표현하고 받아들임
        - 문자를 숫자로 표현하는 규약 ASCIIcode를 만들어 128개의 문자를 숫자와 일대일 매칭
        - 따라서 문자에 대응되는 숫자데이터가 bianry digit으로 표현되어 메모리에 저장됨

## 자료구조
데이터를 저장하고 관리하는 방식

- Array vs Linked List
    - Array
        - 데이터가 연속적으로 저장
        - **데이터의 접근이 쉬움**
        - 데이터 저장
            - int array[4] = {5, 6, 7, 8}
            - 각 4byte 씩(총 16byte)
            - 각 데이터는 가장 작은 address를 대표 주소값으로 설정
    - Linked List
        - 메모리상에 불연속적으로 저장되지만 다음 데이터의 address를 저장하여 연속성 유지
        - **데이터 추가 / 삭제 용이**
        - node: value / address를 저장한 구조체
            - value, address 각각 4byte 가정했을 때 하나의 노드는 8byte

  
  Reference(https://www.youtube.com/watch?v=JHxY08iENxs&t=4s)