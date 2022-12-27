# 5-1. 클래스  

## **클래스는 왜 필요한가?**

프로그래머들이 가장 많이 사용하는 프로그래밍 언어 중 하나인 C 언어에는 클래스가 없다.

이 말은 굳이 클래스가 없어도 프로그램을 충분히 만들 수 있다는 뜻이다.

파이썬으로 잘 만든 프로그램을 살펴보아도 클래스를 사용하지 않고 작성한 것들이 상당히 많다.

클래스는 지금까지 공부한 함수나 자료형처럼 프로그램 작성을 위해 꼭 필요한 요소는 아니다.

하지만 프로그램을 작성할 때 클래스를 적재적소에 사용하면 프로그래머가 얻을 수 있는 이익은 상당하다.

계산기는 이전에 계산한 결괏값을 항상 메모리 어딘가에 저장하고 있어야 한다.

```python
result = 0

def add(num):
global result
    result += num
return result

print(add(3))
print(add(4))
```

이전에 계산한 결괏값을 유지하기 위해서 result 전역 변수(global)를 사용했다.

<br>

```python
result1 = 0
result2 = 0

def add1(num):
global result1
    result1 += num
return result1

def add2(num):
global result2
    result2 += num
return result2

print(add1(3))
print(add1(4))
print(add2(3))
print(add2(7))
```

똑같은 일을 하는 add1과 add2 함수를 만들었고 각 함수에서 계산한 결괏값을 유지하면서 저장하는 전역 변수 result1, result2가 필요하게 되었다.

계산기 1의 결괏값이 계산기 2에 아무 영향을 끼치지 않음을 확인할 수 있다.

하지만 계산기가 3개, 5개, 10개로 점점 더 많이 필요해진다면,

여기에 계산기마다 빼기나 곱하기와 같은 기능을 추가해야 한다면 상황은 점점 더 어려워질 것이다.

<br>

클래스를 사용하면 다음과 같이 간단하게 해결할 수 있다.

```python
classCalculator:
def __init__(self):
        self.result = 0

def add(self, num):
        self.result += num
				return self.result

cal1 = Calculator()
cal2 = Calculator()

print(cal1.add(3))
print(cal1.add(4))
print(cal2.add(3))
print(cal2.add(7))
```

프로그램을 실행하면 함수 2개를 사용했을 때와 동일한 결과가 출력된다.

<br>

Calculator 클래스로 만든 별개의 계산기 cal1, cal2(파이썬에서는 이것을 객체라고 부름)가 각각의 역할을 수행한다.

그리고 계산기(cal1, cal2)의 결괏값 역시 다른 계산기의 결괏값과 상관없이 독립적인 값을 유지한다.

클래스를 사용하면 계산기 대수가 늘어나더라도 객체를 생성만 하면 되기 때문에 함수를 사용하는 경우와 달리 매우 간단해진다. 

만약 빼기 기능을 더하려면 Calculator 클래스에 다음과 같은 빼기 기능 함수를 추가해 주면 된다.

```python
class Calculator:
def __init__(self):
        self.result = 0

def add(self, num):
        self.result += num
				return self.result

def sub(self, num):
        self.result -= num
				return self.result
```

<br>

## **클래스와 객체**

- 과자 틀 → 클래스 (class)
- 과자 틀에 의해서 만들어진 과자 → 객체 (object)

여기에서 설명할 클래스는 과자 틀과 비슷하다.

클래스(class)란 똑같은 무엇인가를 계속해서 만들어 낼 수 있는 설계 도면이고(과자 틀), 

객체(object)란 클래스로 만든 피조물(과자 틀을 사용해 만든 과자)을 뜻한다.

클래스로 만든 객체는 각각 고유한 성격을 가진다는  중요한 특징이 있다.

동일한 클래스로 만든 객체일지라도, 서로 전혀 영향을 주지 않는다.

```python
>>> class Cookie:
>>> pass
```

객체는 클래스로 만들며 1개의 클래스는 무수히 많은 객체를 만들어 낼 수 있다.

```python
>>> a = Cookie()
>>> b = Cookie()
```

`Cookie()`의 결괏값을 돌려받은 a와 b가 바로 객체이다.

마치 함수를 사용해서 그 결괏값을 돌려받는 모습과 비슷하다.

<br>

**객체와 인스턴스의 차이**

클래스로 만든 객체를 인스턴스라고도 한다.

a = Cookie() 이렇게 만든 a는 객체이다.

그리고 a 객체는 Cookie의 인스턴스이다.

즉 인스턴스라는 말은 특정 객체(a)가 어떤 클래스(Cookie)의 객체인지를 관계 위주로 설명할 때 사용한다.

"a는 인스턴스"보다는 "a는 객체"라는 표현이 어울리며 "a는 Cookie의 객체"보다는 "a는 Cookie의 인스턴스"라는 표현이 훨씬 잘 어울린다.

<br>

## **사칙연산 클래스 만들기**

### **클래스를 어떻게 만들지 먼저 구상하기**

클래스는 무작정 만드는 것보다 클래스로 만든 객체를 중심으로 어떤 식으로 동작하게 할것인지 미리 구상을 한 후에 생각한 것들을 하나씩 해결하면서 완성해 나가는 것이 좋다.

먼저 `a = FourCal()`를 입력해서 a라는 객체를 만든다.

```python
>>> a = FourCal()
```

그런 다음 `a.setdata(4, 2)`처럼 입력해서 숫자 4와 2를 a에 지정해 주고

```python
>>> a.setdata(4, 2)
```

`a.add()`를 수행하면 두 수를 합한 결과(`4 + 2`)를 리턴하고

```python
>>> print(a.add())
6
```

`a.mul()`을 수행하면 두 수를 곱한 결과(`4 * 2`)를 리턴하고

```python
>>> print(a.mul())
8
```

`a.sub()`를 수행하면 두 수를 뺀 결과(`4 - 2`)를 리턴하고

```python
>>> print(a.sub())
2
```

`a.div()`를 수행하면 두 수를 나눈 결과(`4 / 2`)를 리턴한다.

```python
>>> print(a.div())
2
```

### **클래스 구조 만들기**

제일 먼저 할 일은 `a = FourCal()`처럼 객체를 만들 수 있게 하는 것이다. 

일단은 아무 기능이 없어도 되기 때문에 매우 간단하게 만들 수 있다. 다음을 따라 해 보자.

```python
>>> class FourCal:
...     pass
...
>>>
```

우선 대화형 인터프리터에서 pass란 문장만을 포함한 FourCal 클래스를 만든다.

현재 상태에서 FourCal 클래스는 아무 변수나 함수도 포함하지 않지만 우리가 원하는 객체 a를 만들 수 있는 기능은 가지고 있다.

> pass는 아무것도 수행하지 않는 문법으로 임시로 코드를 작성할 때 주로 사용한다.
> 

```python
>>> a = FourCal()
>>> type(a)
<class '__main__.FourCal'>
```

위와 같이 `a = FourCal()`로 a 객체를 먼저 만들고 그다음에 `type(a)`로 a 객체가 어떤 타입인지 알아보았다.

객체 a가 FourCal 클래스의 인스턴스임을 알 수 있다.

> type 함수는 파이썬이 자체로 가지고 있는 내장 함수로 객체의 타입을 출력한다.
> 

### **객체에 숫자 지정할 수 있게 만들기**

이제 더하기, 나누기, 곱하기, 빼기등의 기능을 하는 객체를 만들어야 한다.

그런데 이러한 기능을 갖춘 객체를 만들려면 우선 a 객체에 사칙연산을 할 때 사용할 2개의 숫자를 먼저 알려주어야 한다.

```python
>>> a.setdata(4, 2)
```

```python
>>> class FourCal:
... def setdata(self, first, second):
...         self.first = first
...         self.second = second
...
>>>

```

앞에서 만든 FourCal 클래스에서 pass 문장을 삭제하고 그 대신 setdata 함수를 만들었다.

클래스 안에 구현된 함수는 다른 말로 **메서드**(Method)라고 부른다.

일반적인 함수를 만들 때 다음과 같이 작성한다.

```python
def 함수명(매개변수):
    수행할 문장
    ...
```

메서드도 클래스에 포함되어 있다는 점만 제외하면 일반 함수와 다를 것이 없다.

setdata 메서드를 다시 보면 다음과 같다.

```python
def setdata(self, first, second):   # 메서드의 매개변수
    self.first = first              # 메서드의 수행문
    self.second = second            # 메서드의 수행문

```

**setdata 메서드의 매개변수**

setdata 메서드는 매개변수로 self, first, second 3개의 입력값을 받는다.

그런데 일반 함수와는 달리 메서드의 첫 번째 매개변수 self는 특별한 의미를 가진다.

다음과 같이 a 객체를 만들고 a 객체를 통해 setdata 메서드를 호출해 보자.

```python
>>> a = FourCal()
>>> a.setdata(4, 2)
```

> 객체를 통해 클래스의 메서드를 호출하려면 a.setdata(4, 2)와 같이 도트(.) 연산자를 사용해야 한다.
> 

setdata 메서드에는 self, first, second 총 3개의 매개변수가 필요한데 실제로는 `a.setdata(4, 2)`처럼 2개 값만 전달했다. 

그 이유는 `a.setdata(4, 2)`처럼 호출하면 setdata 메서드의 첫 번째 매개변수 self에는 setdata메서드를 호출한 객체 a가 자동으로 전달되기 때문이다.

다음 그림을 보면 객체를 호출할 때 입력한 값이 메서드에 어떻게 전달되는지 쉽게 이해할 수 있을 것이다.

![https://wikidocs.net/images/page/12392/setdata.png](https://wikidocs.net/images/page/12392/setdata.png)

파이썬 메서드의 첫 번째 매개변수 이름은 관례적으로 self를 사용한다.

객체를 호출할 때 호출한 객체 자신이 전달되기 때문에 self라는 이름를 사용한 것이다.

물론 self말고 다른 이름을 사용해도 상관없다.

> 메서드의 첫 번째 매개변수 self를 명시적으로 구현하는 것은 파이썬만의 독특한 특징이다. 예를 들어 자바 같은 언어는 첫 번째 매개변수 self가 필요없다.
> 

**메서드의 또 다른 호출 방법**
잘 사용하지는 않지만 다음과 같이 클래스를 통해 메서드를 호출하는 것도 가능하다.

```python
>>> a = FourCal()
>>> FourCal.setdata(a, 4, 2)
```

위와 같이 클래스이름.메서드 형태로 호출할 때는 객체 a를 첫 번째 매개변수 self에 꼭 전달해 주어야 한다.

반면에 다음처럼 `객체.메서드` 형태로 호출할 때는 self를 반드시 생략해서 호출해야 한다.

```python
>>> a = FourCal()
>>> a.setdata(4, 2)
```

**setdata 메서드의 수행문**

```python
def setdata(self, first, second):   # 메서드의 매개변수
    self.first = first              # 메서드의 수행문
    self.second = second            # 메서드의 수행문
```

`a.setdata(4, 2)`처럼 호출하면 setdata 메서드의 매개변수 first, second에는 각각 값 4와 2가 전달되어 setdata 메서드의 수행문은 다음과 같이 해석된다.

```python
self.first = 4
self.second = 2
```

self는 전달된 객체 a이므로 다시 다음과 같이 해석된다.

```python
a.first = 4
a.second = 2
```

`a.first = 4` 라는 문장이 수행되면 a 객체에 객체변수 first가 생성되고 4라는 값이 저장된다.

마찬가지로 `a.second = 2` 라는 문장이 수행되면 a 객체에 객체변수 second가 생성되고 2라는 값이 저장된다.

> 객체에 생성되는 객체만의 변수를 객체변수라고 부른다.
> 

```python
>>> a = FourCal()
>>> a.setdata(4, 2)
>>> print(a.first)
4
>>> print(a.second)
2
```

```python
>>> a = FourCal()
>>> b = FourCal()
```

```python
>>> a.setdata(4, 2)
>>> print(a.first)
4
```

```python
>>> b.setdata(3, 7)
>>> print(b.first)
3
```

```python
>>> print(a.first)
4
```

클래스로 만든 객체의 객체변수는 다른 객체의 객체변수에 상관없이 독립적인 값을 유지한다.

클래스에서는 이 부분을 이해하는 것이 가장 중요하다.

현재까지 완성된 FourCal 클래스이다.

```python
>>> classFourCal:
... def setdata(self, first, second):
...         self.first = first
...         self.second = second
...
>>>
```

### **더하기 기능 만들기**

자! 그럼 2개의 숫자 값을 설정해 주었으니 2개의 숫자를 더하는 기능을 방금 만든 클래스에 추가해 보자. 우리는 다음과 같이 더하기 기능을 갖춘 클래스를 만들어야 한다.

```python
>>> a = FourCal()
>>> a.setdata(4, 2)
>>> print(a.add())
6
```

이 연산이 가능하도록 다음과 같이 FourCal 클래스를 만들어 보자.

```python
>>> class FourCal:
... def setdata(self, first, second):
...         self.first = first
...         self.second = second
... def add(self):
...         result = self.first + self.second
... return result
...
>>>
```

```python
>>> a = FourCal()
>>> a.setdata(4, 2)
```

```python
>>> print(a.add())
>>> 6
```

`a.add()`라고 호출하면 add 메서드가 호출되어 값 6이 출력될 것이다.

```python
def add(self):
    result = self.first + self.second
return result
```

```python
result = self.first + self.second
```

`a.add()`와 같이 a 객체에 의해 add 메서드가 수행되면 add 메서드의 self에는 객체 a가 자동으로 입력되므로 위 내용은 다음과 같이 해석된다.

```python
result = a.first + a.second
```

위 내용은 `a.add()` 메서드 호출 전에 `a.setdata(4, 2)` 가 먼저 호출되어 `a.first = 4, a.second = 2` 라고 이미 설정되었기 때문에 다시 다음과 같이 해석된다.

```python
result = 4 + 2
```

따라서 다음과 같이 `a.add()`를 호출하면 6을 리턴한다.

```python
>>> print(a.add())
6
```

### **곱하기, 빼기, 나누기 기능 만들기**

```python
>>> class FourCal:
... def setdata(self, first, second):
...         self.first = first
...         self.second = second
... def add(self):
...         result = self.first + self.second
... return result
... def mul(self):
...         result = self.first * self.second
... return result
... def sub(self):
...         result = self.first - self.second
... return result
... def div(self):
...         result = self.first / self.second
...return result
...
>>>
```

```python
>>> a = FourCal()
>>> b = FourCal()
>>> a.setdata(4, 2)
>>> b.setdata(3, 8)
>>> a.add()
6
>>> a.mul()
8
>>> a.sub()
2
>>> a.div()
2
>>> b.add()
11
>>> b.mul()
24
>>> b.sub()
-5
>>> b.div()
0.375
```

<br>

## **생성자 (Constructor)**

```python
>>> a = FourCal()
>>> a.add()
Traceback (most recent call last):
  File "<stdin>", line 1,in <module>
  File "<stdin>", line 6,in add
AttributeError: 'FourCal' object has no attribute 'first'
```

FourCal 클래스의 인스턴스 a에 setdata 메서드를 수행하지 않고 add 메서드를 먼저 수행하면 "AttributeError: 'FourCal' object has no attribute 'first'" 오류가 발생한다.

왜냐하면 setdata 메서드를 수행해야 객체 a의 객체변수 first와 second가 생성되기 때문이다.

이렇게 객체에 first, second와 같은 초깃값을 설정해야 할 필요가 있을 때는 setdata와 같은 메서드를 호출하여 초깃값을 설정하기보다는 생성자를 구현하는 것이 안전한 방법이다.

생성자(Constructor)란 객체가 생성될 때 자동으로 호출되는 메서드를 의미한다.

파이썬 메서드 이름으로 `__init__`를 사용하면 이 메서드는 생성자가 된다.

> __init__ 메서드의 init 앞뒤로 붙은 __는 언더스코어(_) 두 개
> 

```python
>>> class FourCal:
... def __init__(self, first, second):
...         self.first = first
...         self.second = second
... def setdata(self, first, second):
...         self.first = first
...         self.second = second
... def add(self):
...         result = self.first + self.second
... return result
... def mul(self):
...         result = self.first * self.second
... return result
... def sub(self):
...         result = self.first - self.second
... return result
... def div(self):
...         result = self.first / self.second
... return result
...
>>>
```

새롭게 추가된 생성자 `__init__` 메서드만 따로 떼어 내서 살펴보자.

```python
def__init__(self, first, second):
    self.first = first
    self.second = second
```

`__init__` 메서드는 setdata 메서드와 이름만 다르고 모든 게 동일하다.

단 메서드 이름을 `__init__`으로 했기 때문에 생성자로 인식되어 객체가 생성되는 시점에 자동으로 호출되는 차이가 있다.

이제 다음처럼 예제를 수행해 보자.

```python
>>> a = FourCal()
Traceback (most recent call last):
  File "<stdin>", line 1,in <module>
TypeError: __init__() missing 2 required positional arguments: 'first'and 'second'
```

`a = FourCal()`을 수행할 때 생성자 `__init__`이 호출되어 위와 같은 오류가 발생했다.

오류가 발생한 이유는 생성자의 매개변수 first와 second에 해당하는 값이 전달되지 않았기 때문이다.

위 오류를 해결하려면 다음처럼 first와 second에 해당되는 값을 전달하여 객체를 생성해야 한다.

```python
>>> a = FourCal(4, 2)
>>>
```

위와 같이 수행하면 `__init__` 메서드의 매개변수에는 각각 다음과 같은 값이 전달된다.

| 매개변수 | 값 |
| --- | --- |
| self | 생성되는 객체 |
| first | 4 |
| second | 2 |

> __init__ 메서드도 다른 메서드와 마찬가지로 첫 번째 매개변수 self에 생성되는 객체가 자동으로 전달된다는 점을 기억하자.
> 

따라서 `__init__` 메서드가 호출되면 setdata 메서드를 호출했을 때와 마찬가지로 first와 second라는 객체변수가 생성될 것이다.

```python
>>> a = FourCal(4, 2)
>>> print(a.first)
4
>>> print(a.second)
2
```

```python
>>> a = FourCal(4, 2)
>>> a.add()
6
>>> a.div()
2.0
```

<br>

## **클래스의 상속**

상속(Inheritance)이란 "물려받다"라는 뜻으로, "재산을 상속받다"라고 할 때의 상속과 같은 의미이다.

클래스에도 이 개념을 적용할 수 있다.

어떤 클래스를 만들 때 다른 클래스의 기능을 물려받을 수 있게 만드는 것이다.

이번에는 상속 개념을 사용하여 우리가 만든 FourCal 클래스에 ab (a의 b제곱)을 구할 수 있는 기능을 추가해 보자.

앞에서 FourCal 클래스는 이미 만들어 놓았으므로 FourCal 클래스를 상속하는 MoreFourCal 클래스는 다음과 같이 간단하게 만들 수 있다.

```python
>>> class MoreFourCal(FourCal):
...     pass
...
>>>
```

클래스를 상속하기 위해서는 다음처럼 클래스 이름 뒤 괄호 안에 상속할 클래스 이름을 넣어주면 된다.

> class 클래스 이름(상속할 클래스 이름)
> 

MoreFourCal 클래스는 FourCal 클래스를 상속했으므로 FourCal 클래스의 모든 기능을 사용할 수 있어야 한다.

다음과 같이 확인해 보자.

```python
>>> a = MoreFourCal(4, 2)
>>> a.add()
6
>>> a.mul()
8
>>> a.sub()
2
>>> a.div()
2
```

상속받은 FourCal 클래스의 기능을 모두 사용할 수 있음을 확인할 수 있다.

<br>

**왜 상속을 해야 할까?**
보통 상속은 기존 클래스를 변경하지 않고 기능을 추가하거나 기존 기능을 변경하려고 할 때 사용한다.
"클래스에 기능을 추가하고 싶으면 기존 클래스를 수정하면 되는데 왜 굳이 상속을 받아서 처리해야 하지?" 라는 의문이 들 수도 있다. 

하지만 기존 클래스가 라이브러리 형태로 제공되거나 수정이 허용되지 않는 상황이라면 상속을 사용해야 한다.

이제 원래 목적인 a의 b제곱(ab)을 계산하는 MoreFourCal 클래스를 만들어 보자.

```python
>>> class MoreFourCal(FourCal):
... def pow(self):
...         result = self.first ** self.second
... return result
...
>>>
```

pass 문장은 삭제하고 위와 같이 두 수의 거듭제곱을 구할 수 있는 pow 메서드를 추가했다.

그리고 다음과 같이 pow 메서드를 수행해 보자.

```python
>>> a = MoreFourCal(4, 2)
>>> a.pow()
16
>>> a.add()
6
```

MoreFourCal 클래스로 만든 a 객체에 값 4와 2를 설정한 후 pow 메서드를 호출하면 4의 2제곱 (42)인 16을 리턴하는 것을 확인할 수 있다. 

상속받은 기능인 add 메서드도 역시 잘 동작한다.

상속은 MoreFourCal 클래스처럼 기존 클래스(FourCal)는 그대로 놔둔 채 클래스의 기능을 확장시킬 때 주로 사용한다.

<br>

## **메서드 오버라이딩**

```python
>>> a = FourCal(4, 0)
>>> a.div()
Traceback (most recent call last):
  File "<stdin>", line 1,in <module>
    result = self.first / self.second
ZeroDivisionError: division by zero
```

FourCal 클래스의 객체 a에 4와 0 값을 설정하고 div 메서드를 호출하면 4를 0으로 나누려고 하기 때문에 위와 같은 ZeroDivisionError 오류가 발생한다.

하지만 0으로 나눌 때 오류가 아닌 0을 리턴하도록 만들고 싶다면 어떻게 해야 할까?

다음과 같이 FourCal 클래스를 상속하는 SafeFourCal 클래스를 만들어 보자.

```python
>>>class SafeFourCal(FourCal):
... def div(self):
... if self.second == 0:  # 나누는 값이 0인 경우 0을 리턴하도록 수정
... return 0
... else:
... return self.first / self.second
...
>>>
```

SafeFourCal 클래스는 FourCal 클래스에 있는 div 메서드를 동일한 이름으로 다시 작성하였다.

이렇게 부모 클래스(상속한 클래스)에 있는 메서드를 동일한 이름으로 다시 만드는 것을 **메서드 오버라이딩**(Overriding, 덮어쓰기)이라고 한다.

이렇게 메서드를 오버라이딩하면 부모클래스의 메서드 대신 오버라이딩한 메서드가 호출된다.

```python
>>> a = SafeFourCal(4, 0)
>>> a.div()
0
```

FourCal 클래스와는 달리 ZeroDivisionError가 발생하지 않고 의도한 대로 0이 리턴되는 것을 확인할 수 있다.

<br>

## **클래스 변수**

객체변수는 다른 객체들의 영향을 받지 않고 독립적으로 그 값을 유지한다는 점을 이미 알아보았다.

이번에는 객체변수와는 성격이 다른 클래스 변수에 대해 알아보자.

다음 클래스를 작성해 보자.

```python
>>> class Family:
...     lastname = "김"
...
```

Family 클래스에 선언한 lastname이 바로 클래스 변수이다.

클래스 변수는 클래스 안에 함수를 선언하는 것과 마찬가지로 클래스 안에 변수를 선언하여 생성한다.

```python
>>> print(Family.lastname)
김
```

클래스 변수는 위 예와 같이 `클래스이름.클래스변수`로 사용할 수 있다.

또는 다음과 같이 Family 클래스로 만든 객체를 통해서도 클래스 변수를 사용할 수 있다.

```python
>>> a = Family()
>>> b = Family()
>>> print(a.lastname)
김
>>> print(b.lastname)
김
```

만약 Family 클래스의 lastname을 다음과 같이 "박"이라는 문자열로 바꾸면 어떻게 될까?

```python
>>> Family.lastname = "박"
```

```python
>>> print(a.lastname)
박
>>> print(b.lastname)
박
```

클래스 변수 값을 변경했더니 클래스로 만든 객체의 lastname 값도 모두 변경된다.

클래스 변수는 클래스로 만든 모든 객체에 공유된다는 특징이 있다.

**클래스 변수와 동일한 이름의 객체 변수를 생성하면?**
위의 예제에서 `a.lastname`을 다음처럼 변경하면 어떻게 될까?

```python
>>> a.lastname = "최"
>>> print(a.lastname)
최
```

이렇게 하면 Family 클래스의 lastname이 바뀌는 것이 아니라 a 객체에 lastname이라는 객체변수가 새롭게 생성된다.

즉, 객체변수는 클래스 변수와 동일한 이름으로 생성할 수 있다.
`a.lastname` 객체변수를 생성하더라도 Family 클래스의 lastname과는 상관없다는 것을 다음과 같이 확인할 수 있다.

```python
>>> print(Family.lastname)
박
>>> print(b.lastname)
박
```

Family 클래스의 lastname 값은 변하지 않았다.

클래스 변수를 가장 늦게 설명하는 이유는 클래스에서 클래스 변수보다는 객체변수가 훨씬 중요하기 때문이다.

실무 프로그래밍을 할 때도 클래스 변수보다는 객체변수를 사용하는 비율이 훨씬 높다.

<br>

출처: 점프 투 파이썬 - 박응용
