# 4-1. 함수

입력(x) 값에 따라 출력(y) 값이 변하는 상자...

## **함수를 사용하는 이유**

프로그래밍을 하다 보면 똑같은 내용을 반복해서 작성하고 있는 자신을 발견할 때가 종종 있다.

반복되는 부분이 있을 경우 "반복적으로 사용되는 가치 있는 부분"을 한 뭉치로 묶어서

"어떤 입력값을 주었을 때 어떤 결괏값을 돌려준다"라는 식의 함수로 작성하는 것.

함수를 사용하는 또 다른 이유는 자신이 작성한 프로그램을 기능 단위의 함수로 분리해 놓으면 

프로그램 흐름을 일목요연하게 볼 수 있기 때문이다. 

마치 공장에서 원재료가 여러 공정을 거쳐 하나의 완제품이 되는 것처럼 프로그램에서도 입력한 값이 

여러 함수를 거치면서 원하는 결괏값을 내는 것을 볼 수 있다. 

이렇게 되면 프로그램 흐름도 잘 파악할 수 있고 오류가 어디에서 나는지도 쉽게 알아차릴 수 있다.

<br>

## **파이썬 함수의 구조**

파이썬 함수의 구조는 다음과 같다.

```python
def 함수명(매개변수):
    <수행할 문장1>
    <수행할 문장2>
    ...
```

def는 함수를 만들 때 사용하는 예약어이며, 함수명은 함수를 만드는 사람이 임의로 만들 수 있다.

함수명 뒤 괄호 안의 매개변수는 이 함수에 입력으로 전달되는 값을 받는 변수이다.

이렇게 함수를 정의한 다음 if, while, for문 등과 마찬가지로 함수에서 수행할 문장을 입력한다.

```python
def add(a, b):
return a + b
```

여기에서 return은 함수의 결괏값(리턴값)을 돌려주는 명령어이다.

```python
>>> def add(a, b):
... return a + b
...
>>>
```

```python
>>> a = 3
>>> b = 4
>>> c = add(a, b)
>>> print(c)
7
```

<br>

## **매개변수와 인수**

매개변수와 인수는 혼용해서 사용되는 헷갈리는 용어이므로 잘 기억해 두자. 

매개변수는 함수에 입력으로 전달된 값을 받는 변수를 의미하고 인수는 함수를 호출할 때 전달하는 입력값을 의미한다.

```python
defadd(a, b):  # a, b는 매개변수
return a+b

print(add(3, 4))  # 3, 4는 인수
```

- 매개변수 - 함수에 전달된 값을 저장하는 변수
- 인수 - 함수에 전달하는 값

<br>

## **입력값과 리턴값에 따른 함수의 형태**

> 입력값 ---> 함수 ----> 리턴값
> 

함수의 형태는 입력값과 리턴값의 존재 유무에 따라 4가지 유형으로 나뉜다. 

### **일반적인 함수**

입력값이 있고 리턴값이 있는 함수가 일반적인 함수이다.

```python
def 함수이름(매개변수):
    <수행할 문장>
    ...
return 리턴값
```

```python
defadd(a, b):
    result = a + b
return result
```

```python
>>> a = add(3, 4)
>>> print(a)
7
```

이처럼 입력값과 리턴값이 있는 함수의 사용법을 정리하면 다음과 같다.

> 리턴값을 받을 변수 = 함수이름(입력인수1, 입력인수2, ...)
> 

<br>

### **입력값이 없는 함수**

```python
>>> def say():
... return 'Hi'
...
>>>
```

```python
>>> a = say()
>>> print(a)
Hi
```

> 리턴값을 받을 변수 = 함수이름()
> 

<br>

### **리턴값이 없는 함수**

```python
>>> def add(a, b):
...     print("%d, %d의 합은 %d입니다." % (a, b, a+b))
...
>>>
```

```python
>>> add(3, 4)
3, 4의 합은 7입니다.
```

```python
>>> a = add(3, 4)
3, 4의 합은 7입니다.
```

"3, 4의 합은 7입니다." 라는 문장을 출력해 주었는데 왜 리턴값이 없다는 것인지 의아하게 생각할 수도 있다. 

이 부분이 초보자들이 혼란스러워하는 부분이기도 한데 print문은 함수의 구성 요소 중 하나인 `<수행할 문장>`에 해당하는 부분일 뿐이다. 

리턴값은 오직 return 명령어로만 돌려받을 수 있다.

리턴받을 값을 a 변수에 대입하여 출력해 보면 리턴값이 있는지 없는지 알 수 있다.

```python
>>> a = add(3, 4)
3, 4의 합은 7입니다.
>>> print(a)
None

```

a 값으로 None이 출력되었다. None이란 거짓을 나타내는 자료형이라고 언급한 적이 있다.

add 함수처럼 리턴값이 없을 때 `a = add(3, 4)`처럼 쓰면 함수 add는 리턴값으로 a 변수에 None을 리턴한다. 

<br>

### **입력값도 리턴값도 없는 함수**

```python
>>> def say():
...     print('Hi')
...
>>>
```

```python
>>> say()
Hi
```

<br>

## **매개변수 지정하여 호출하기**

```python
>>> def sub(a, b):
... return a - b
...
```

두 개의 숫자를 입력 받아 첫번째 수에서 두번째 수를 뺄셈하여 리턴하는 sub 함수이다. 

이 함수를 다음과 같이 매개변수를 지정하여 사용할 수 있다.

```python
>>> result = sub(a=7, b=3)  # a에 7, b에 3을 전달
>>> print(result)
4
```

매개변수를 지정하면 다음과 같이 순서에 상관없이 사용할 수 있다는 장점이 있다.

```python
>>> result = sub(b=5, a=3)  # b에 5, a에 3을 전달
>>> print(result)
-2
```

<br>

## **입력값이 몇 개가 될지 모를 때**

입력값이 여러 개일 때 그 입력값을 모두 더해 주는 함수

```python
def 함수이름(*매개변수):
    <수행할 문장>
    ...
```

일반적으로 볼 수 있는 함수 형태에서 괄호 안의 매개변수 부분이 `*매개변수`로 바뀌었다.

<br>

**여러 개의 입력값을 받는 함수 만들기**

```python
>>> def add_many(*args):
...     result = 0
... for i in args:
...         result = result + i
... return result
...
>>>
```

`*args`처럼 매개변수 이름 앞에 `*`을 붙이면 입력값을 전부 모아서 튜플로 만들어준다.

```python
>>> result = add_many(1,2,3)
>>> print(result)
6
>>> result = add_many(1,2,3,4,5,6,7,8,9,10)
>>> print(result)
55
```

여러 개의 입력을 처리할 때 `def add_many(*args)`처럼 함수의 매개변수로 `*args` 하나만 사용할 수 있는 것은 아니다.

```python
>>> def add_mul(choice, *args):
... if choice == "add":
...         result = 0
... for i in args:
...             result = result + i
... elif choice == "mul":
...         result = 1
... for i in args:
...             result = result * i
... return result
...
>>>
```

```python
>>> result = add_mul('add', 1,2,3,4,5)
>>> print(result)
15
>>> result = add_mul('mul', 1,2,3,4,5)
>>> print(result)
120
```

<br>

## **키워드 매개변수 kwargs**

키워드 매개변수를 사용할 때는 매개변수 앞에 별 두 개(`**`)를 붙인다.

```python
>>> def print_kwargs(**kwargs):
...     print(kwargs)
...
```

```python
>>> print_kwargs(a=1)
{'a': 1}
>>> print_kwargs(name='foo', age=3)
{'age': 3, 'name': 'foo'}

```

함수의 입력값으로 `a=1`이 사용되면 kwargs는 `{'a': 1}`이라는 딕셔너리가 되고,

입력값으로 `name='foo', age=3`이 사용되면 kwargs는 `{'age': 3, 'name': 'foo'}`라는 딕셔너리가 된다. 

즉, `**kwargs`처럼 매개변수 이름 앞에 `**`을 붙이면 매개변수 kwargs는 딕셔너리가 되고 모든 `key=value` 형태의 입력값이 그 딕셔너리에 저장된다.

> kwargs는 keyword arguments의 약자이며 args와 마찬가지로 관례적으로 사용한다.
> 

<br>

## **함수의 리턴값은 언제나 하나이다**

```python
>>> def add_and_mul(a,b):
... return a + b, a * b
```

```python
result = (7, 12)
```

만약 이 하나의 튜플 값을 2개의 값으로 분리하여 받고 싶다면 다음과 같이 함수를 호출하면 된다.

```python
>>> result1, result2 = add_and_mul(3, 4)
```

이렇게 호출하면 `result1, result2 = (7, 12)`가 되어 result1은 7이 되고 result2는 12가 된다.

```python
>>> def add_and_mul(a, b):
... return a + b
... return a * b
...
>>>
```

```python
>>> result = add_and_mul(2, 3)
>>> print(result)
5
```

`add_and_mul(2, 3)`의 리턴값은 5 하나뿐이다. 

두 번째 return문인 `return a*b`는 실행되지 않았다는 뜻이다. 따라서 이 함수는 다음과 완전히 동일하다.

```python
>>> def add_and_mul(a,b):
...return a+b
...
>>>
```

즉 함수는 return문을 만나는 순간 리턴값을 돌려준 다음 함수를 빠져나가게 된다.

<br>

## **매개변수에 초깃값 미리 설정하기**

```python
def say_myself(name, age, man=True):
    print("나의 이름은 %s 입니다." % name)
    print("나이는 %d살입니다." % age)
if man:
        print("남자입니다.")
else:
        print("여자입니다.")
```

say_myself 함수는 다음처럼 2가지 방법으로 사용할 수 있다.

```python
say_myself("박응용", 27)
say_myself("박응용", 27, True)
```

```python
나의 이름은 박응용입니다.
나이는 27살입니다.
남자입니다.
```

cf.

```python
say_myself("박응선", 27, False)
```

```python
나의 이름은 박응선입니다.
나이는 27살입니다.
여자입니다.
```

<br>

이것은 함수를 실행할 때 오류가 발생한다.

```python
def say_myself(name,man=True, age):
    print("나의 이름은 %s 입니다." % name)
    print("나이는 %d살입니다." % age)
if man:
        print("남자입니다.")
else:
        print("여자입니다.")
```

얼핏 생각하기에 위 함수를 호출하려면 다음과 같이 하면 될 것 같다.

```python
say_myself("박응용", 27)
```

위와 같이 함수를 호출한다면 name 변수에는 "박응용"이 들어갈 것이다.

하지만 파이썬 인터프리터는 27을 man 매개변수와 age 매개변수 중 어느 곳에 대입해야 할지 판단하기가 어려워 이러한 상황에서는 오류를 발생시키게 했다.

```python
SyntaxError: non-default argument follows default argument
```

위 오류 메시지는 초깃값이 없는 매개변수(age)는 초깃값이 있는 매개변수(man) 뒤에 사용할 수 없다는 뜻이다. 

초기화시키고 싶은 매개변수는 항상 뒤쪽에 놓아야 한다.

<br>

## **함수 안에서 선언한 변수의 효력 범위**

```python
# vartest.py
a = 1
def vartest(a):
    a = a +1

vartest(a)
print(a)
```

먼저 a라는 변수를 생성하고 1을 대입했다. 

그리고 입력으로 들어온 값에 1을 더해 주고 결괏값은 리턴하지 않는 vartest 함수를 선언했다. 

그리고 vartest 함수에 입력값으로 a를 주었다. 

마지막으로 a의 값을 `print(a)`로 출력했다.

과연 어떤 값이 출력될까?

vartest 함수에서 매개변수 a의 값에 1을 더했으니까 2가 출력될 것 같지만 프로그램 소스를 작성해서 실행해 보면 결괏값은 1이 나온다. 

그 이유는 함수 안에서 사용하는 매개변수는 함수 안에서만 사용하는 "함수만의 변수"이기 때문이다. 

즉 `def vartest(a)`에서 입력값을 전달받는 매개변수 a는 함수 안에서만 사용하는 변수이지 함수 밖의 변수 a와는 전혀 상관이 없다는 뜻이다.

따라서 vartest 함수는 다음처럼 매개변수 이름을 hello로 바꾸어도 이전의 vartest 함수와 완전히 동일하게 동작한다.

```python
def vartest(hello):
    hello = hello + 1
```

즉 함수 안에서 사용하는 매개변수는 함수 밖의 변수 이름과는 전혀 상관이 없다는 뜻이다.

```python
# vartest_error.py
def vartest(a):
    a = a + 1

vartest(3)
print(a)
```

함수 안에서 선언한 매개변수는 함수 안에서만 사용될 뿐 함수 밖에서는 사용되지 않는다.

<br>

## **함수 안에서 함수 밖의 변수를 변경하는 방법**

**global 명령어 사용하기**

```python
# vartest_global.py
a = 1
defvartest():
global a
    a = a+1

vartest()
print(a)
```

위 예에서 볼 수 있듯이 vartest 함수 안의 `global a` 문장은 함수 안에서 함수 밖의 a 변수를 직접 사용하겠다는 뜻이다.

하지만 프로그래밍을 할 때 global 명령어는 사용하지 않는 것이 좋다.

왜냐하면 함수는 독립적으로 존재하는 것이 좋기 때문이다.

외부 변수에 종속적인 함수는 그다지 좋은 함수가 아니다.

<br>

## **lambda**

lambda는 함수를 생성할 때 사용하는 예약어로 def와 동일한 역할을 한다. 

보통 함수를 한줄로 간결하게 만들 때 사용한다. 

우리말로는 "람다"라고 읽고 def를 사용해야 할 정도로 복잡하지 않거나 def를 사용할 수 없는 곳에 주로 쓰인다.

> 함수명 = lambda 매개변수1, 매개변수2, ... : 매개변수를 이용한 표현식
> 

한번 직접 만들어 보자.

```python
>>> add = lambda a, b: a+b
>>> result = add(3, 4)
>>> print(result)
7
```

> lambda로 만든 함수는 return 명령어가 없어도 표현식의 결괏값을 리턴한다.
> 

add는 두 개의 인수를 받아 서로 더한 값을 리턴하는 lambda 함수이다. 

def를 사용한 다음 함수와 하는 일이 완전히 동일하다.

```python
>>> def add(a, b):
... return a+b
...
```

<br>

출처: 점프 투 파이썬 - 
따라서 vartest 함수는 다음처럼 매개변수 이름을 hello로 바꾸어도 이전의 vartest 함수와 완전히 동일하게 동작한다.
