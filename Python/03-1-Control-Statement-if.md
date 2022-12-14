# 3-1. if

## **if문의 기본 구조**

```python
if 조건문:
    수행할 문장1
    수행할 문장2
    ...
else:
    수행할 문장A
    수행할 문장B
    ...
```

조건문을 테스트해서 참이면 if문 바로 다음 문장(if 블록)들을 수행하고, 

조건문이 거짓이면 else문 다음 문장(else 블록)들을 수행하게 된다. 

그러므로 else문은 if문 없이 독립적으로 사용할 수 없다.

<br>

## **들여쓰기**

if문을 만들 때는 if 조건문: 바로 아래 문장부터 if문에 속하는 모든 문장에 들여쓰기(indentation)를 해주어야 한다. 

```python
if 조건문:
    수행할 문장1
    수행할 문장2
    수행할 문장3
```

```python
money = True
if money:
    print("택시를")
print("타고")
    print("가라")

```

"수행할 문장3"을 들여쓰기했지만 "수행할 문장1"이나 "수행할 문장2"와 들여쓰기의 깊이가 다르다. 

즉 들여쓰기는 언제나 같은 깊이로 해야 한다.

<br>

**조건문 다음에 콜론(:)**
if 조건문 뒤에는 반드시 콜론(:)이 붙는다.

어떤 특별한 의미가 있다기보다는 파이썬의 문법 구조이다. 

왜 하필 콜론(:)인지 궁금하다면 파이썬을 만든 귀도에게 직접 물어봐야 할 것이다. 

앞으로 배울 while이나 for, def, class도 역시 문장의 끝에 콜론(:)이 항상 들어간다. 
파이썬이 다른 언어보다 보기 쉽고 소스 코드가 간결한 이유는 바로 콜론(:)을 사용하여 들여쓰기(indentation)를 하도록 만들었기 때문이다. 

하지만 이는 숙련된 프로그래머들이 파이썬을 처음 접할 때 제일 혼란스러워하는 부분이기도 하다. 

다른 언어에서는 if문에 속한 문장들을 `{ }` 기호로 감싸지만 파이썬에서는 들여쓰기로 해결한다.

<br>

## **조건문이란 무엇인가?**

**if 조건문**에서 "조건문"이란 참과 거짓을 판단하는 문장을 말한다.

앞에서 살펴본 택시 예제에서 조건문은 money가 된다.

```python
>>> money = True
>>> if money:

```

money는 True이기 때문에 조건이 참이 되어 if문 다음 문장을 수행한다.

<br>

### **비교연산자**

| 비교연산자 | 설명 |
| --- | --- |
| x < y | x가 y보다 작다 |
| x > y | x가 y보다 크다 |
| x == y | x와 y가 같다 |
| x != y | x와 y가 같지 않다 |
| x >= y | x가 y보다 크거나 같다 |
| x <= y | x가 y보다 작거나 같다 |

<br>

### **and, or, not**

| 연산자 | 설명 |
| --- | --- |
| x or y | x와 y 둘중에 하나만 참이어도 참이다 |
| x and y | x와 y 모두 참이어야 참이다 |
| not x | x가 거짓이면 참이다 |

<br>

### **in, not in**

| in | not in |
| --- | --- |
| x in 리스트 | x not in 리스트 |
| x in 튜플 | x not in 튜플 |
| x in 문자열 | x not in 문자열 |

```python
>>> 1 in [1, 2, 3]
True
>>> 1 not in [1, 2, 3]
False
```

```python
>>> 'a' in ('a', 'b', 'c')
True
>>> 'j' not in 'python'
True
```

<br>

**조건문에서 아무 일도 하지 않게 설정하고 싶다면**

가끔 조건문의 참, 거짓에 따라 실행할 행동을 정의할 때, 아무런 일도 하지 않도록 설정하고 싶을 때가 있다.
"주머니에 돈이 있으면 가만히 있고 주머니에 돈이 없으면 카드를 꺼내라."
이럴 때 사용하는 것이 바로 pass이다. 

`>>> pocket = ['paper', 'money', 'cellphone']`  
```python
>>> if 'money' in pocket:
...     pass... else:
...     print("카드를 꺼내라")
...
```

pocket 리스트 안에 money 문자열이 있기 때문에 if문 다음 문장인 pass가 수행되고 아무 결괏값도 보여 주지 않는다.

<br>

## **다양한 조건을 판단하는 elif**

> "주머니에 돈이 있으면 택시를 타고, 주머니에 돈은 없지만 카드가 있으면 택시를 타고, 돈도 없고 카드도 없으면 걸어 가라."
> 

if와 else만으로 위 문장을 표현하려면 다음과 같이 할 수 있다.

```python
>>> pocket = ['paper', 'handphone']
>>> card = True
>>> if 'money'in pocket:
...     print("택시를 타고가라")
... else:
... if card:
...         print("택시를 타고가라")
... else:
...         print("걸어가라")
...
택시를 타고가라
>>>
```

<br>

위 예를 elif를 사용하면 다음과 같이 바꿀 수 있다.

```python
>>> pocket = ['paper', 'cellphone']
>>> card = True
>>> if 'money'in pocket:
...      print("택시를 타고가라")
... elif card:
...      print("택시를 타고가라")
... else:
...      print("걸어가라")
...
택시를 타고가라
```

즉 elif는 이전 조건문이 거짓일 때 수행된다. if, elif, else를 모두 사용할 때 기본 구조는 다음과 같다.

```python
if <조건문>:
    <수행할 문장1>
    <수행할 문장2>
    ...
elif <조건문>:
    <수행할 문장1>
    <수행할 문장2>
    ...
elif <조건문>:
    <수행할 문장1>
    <수행할 문장2>
    ...
...
else:
   <수행할 문장1>
   <수행할 문장2>
   ...

```

<br>

**if문을 한 줄로 작성하기**

앞의 pass를 사용한 예를 보면 if문 다음에 수행할 문장이 한 줄이고, else문 다음에 수행할 문장도 한 줄밖에 되지 않는다.

`>>> **if** 'money' **in** pocket:
...     **pass**... **else**:
...     print("카드를 꺼내라")
...`

이렇게 수행할 문장이 한 줄일 때 조금 더 간략하게 코드를 작성

`>>> pocket = ['paper', 'money', 'cellphone']`  
`>>> if 'money' in pocket: pass... else: print("카드를 꺼내라")
...`

<br>

## **조건부 표현식**

다음과 같은 코드를 보자.

```python
if score >= 60:
    message = "success"
else:
    message = "failure"
```

위 코드는 score가 60 이상일 경우 message에 문자열 "success"를, 아닐 경우에는 "failure"를 대입하는 코드이다.

파이썬의 조건부 표현식(conditional expression)을 사용하면 위 코드를 다음과 같이 간단히 표현할 수 있다.

```python
message = "success" if score >= 60 else "failure"
```

조건부 표현식은 다음과 같이 정의한다.

`변수` = `조건문이_참인_경우의_값` if `조건문` else `조건문이_거짓인_경우의_값`

<br>

출처: 점프 투 파이썬 - 박응용
