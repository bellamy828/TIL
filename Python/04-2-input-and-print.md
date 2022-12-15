## **사용자 입력**

### **input의 사용**

```python
>>> a = input()
Life is too short, you need python
>>> a
'Life is too short, you need python'
>>>
```

input은 사용자가 키보드로 입력한 모든 것을 문자열로 저장한다.

<br>

### **프롬프트를 띄워서 사용자 입력 받기**

사용자에게 입력받을 때 "숫자를 입력하세요"라든지 "이름을 입력하세요"라는 

안내 문구 또는 질문이 나오도록 하고 싶을 때가 있다. 

그럴 때는 input()의 괄호 안에 안내문구를 입력하여 프롬프트를 띄워주면 된다.

> input("안내문구")
> 

```python
>>> number = input("숫자를 입력하세요: ")
숫자를 입력하세요:
```

```python
>>> number = input("숫자를 입력하세요: ")
숫자를 입력하세요: 3
>>> print(number)
3
>>>
```

input은 입력되는 모든 것을 문자열로 취급하기 때문에 number는 숫자가 아닌 문자열임에 주의하자.

```python
>>> type(number)
<class 'str'>
>>>
```

<br>

## **print 자세히 알기**

지금껏 우리가 사용한 print 문의 용도는 데이터를 출력하는 것이었다. 

데이터를 출력하는 print 문의 사용예는 다음과 같다.

```python
>>> a = 123
>>> print(a)
123
>>> a = "Python"
>>> print(a)
Python
>>> a = [1, 2, 3]
>>> print(a)
[1, 2, 3]
```

### **큰따옴표(")로 둘러싸인 문자열은 + 연산과 동일하다**

```python
>>> print("life" "is" "too short") # 1
lifeistoo short
>>> print("life"+"is"+"too short") # 2
lifeistoo short
```

### **문자열 띄어쓰기는 콤마로 한다**

```python
>>> print("life", "is", "too short")
lifeis too short
```

### **한 줄에 결괏값 출력하기**

03-3 장에서 for문을 공부할 때 만들었던 구구단 프로그램에서 보았듯이 한 줄에 결괏값을 계속 이어서 출력하려면 매개변수 end를 사용해 끝 문자를 지정해야 한다.

```python
>>> for i in range(10):
...     print(i, end=' ')
...
0 1 2 3 4 5 6 7 8 9
```

> end 매개변수의 초깃값은 줄바꿈(\n) 문자이다.

<br>

출처: 점프 투 파이썬
