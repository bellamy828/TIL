# 3-2. while

## **while문의 기본 구조**

반복해서 문장을 수행해야 할 경우 while문을 사용한다. 그래서 while문을 반복문이라고도 부른다.

```python
while <조건문>:
    <수행할 문장1>
    <수행할 문장2>
    <수행할 문장3>
    ...
```

while문은 조건문이 참인 동안에 while문에 속한 문장들이 반복해서 수행된다.

"열 번 찍어 안 넘어가는 나무 없다"는 속담을 파이썬 프로그램으로 만든다면 다음과 같이 될 것이다.

```python
>>> treeHit = 0
>>> while treeHit < 10:
...     treeHit = treeHit +1
...     print("나무를 %d번 찍었습니다." % treeHit)
... if treeHit == 10:
...         print("나무 넘어갑니다.")
...
나무를 1번 찍었습니다.
나무를 2번 찍었습니다.
나무를 3번 찍었습니다.
나무를 4번 찍었습니다.
나무를 5번 찍었습니다.
나무를 6번 찍었습니다.
나무를 7번 찍었습니다.
나무를 8번 찍었습니다.
나무를 9번 찍었습니다.
나무를 10번 찍었습니다.
나무 넘어갑니다.
```

<br>

## **while문 만들기**

```python
>>> prompt = """
... 1. Add
... 2. Del
... 3. List
... 4. Quit
...
... Enter number: """
>>>
```

이어서 number 변수에 0을 먼저 대입한다. 이렇게 변수를 먼저 설정해놓지 않으면 다음에 나올 while문의 조건문인 `number != 4`에서 변수가 존재하지 않는다는 오류가 발생한다.

```python
>>> number = 0
>>> while number != 4:
...     print(prompt)
...     number = int(input())
...
```

```python
1. Add
2. Del
3. List
4. Quit

Enter number:
```

while문을 보면 number가 4가 아닌 동안 prompt를 출력하고 사용자로부터 번호를 입력받는다. 

다음 결과 화면처럼 사용자가 값 4를 입력하지 않으면 계속해서 prompt를 출력한다.

> 여기에서 number = int(input())는 사용자의 숫자 입력을 받아들이는 것이라고만 알아두자. int나 input 함수에 대한 내용은 뒤의 내장 함수 부분에서 자세하게 다룬다.
> 

<br>

## **while문 강제로 빠져나가기**

```python
>>> coffee = 10
>>> money = 300
>>> while money:
...     print("돈을 받았으니 커피를 줍니다.")
...     coffee = coffee -1
...     print("남은 커피의 양은 %d개입니다." % coffee)
... if coffee == 0:
...         print("커피가 다 떨어졌습니다. 판매를 중지합니다.")
... break
...
```

```python
# coffee.py

coffee = 10
while True:
    money = int(input("돈을 넣어 주세요: "))
if money == 300:
        print("커피를 줍니다.")
        coffee = coffee -1
elif money > 300:
        print("거스름돈 %d를 주고 커피를 줍니다." % (money -300))
        coffee = coffee -1
else:
        print("돈을 다시 돌려주고 커피를 주지 않습니다.")
        print("남은 커피의 양은 %d개 입니다." % coffee)
if coffee == 0:
        print("커피가 다 떨어졌습니다. 판매를 중지 합니다.")
break
```

<br>

## 현재 값을 가지고 **while문의 맨 처음으로 돌아가기**

while문 안의 문장을 수행할 때 입력 조건을 검사해서 조건에 맞지 않으면 while문을 빠져나간다.

그런데 프로그래밍을 하다 보면 while문을 빠져나가지 않고,

현재 비교하는 값을 가지고 다시 while문의 조건문을 확인하고자 할 때 → continue

```python
>>> a = 0
>>> while a < 10:
...     a = a + 1
... if a % 2 == 0:continue...     print(a)
...
1
3
5
7
9
```

<br>

## **무한 루프**

```python
while True:
    수행할 문장1
    수행할 문장2
    ...
```

<br>

출처: 점프 투 파이썬 - 박응용
