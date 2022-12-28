# 5-2. 모듈

모듈이란 함수나 변수 또는 클래스를 모아 놓은 파이썬 파일이다. 

모듈은 다른 파이썬 프로그램에서 불러와 사용할 수 있게끔 만든 파이썬 파일이라고도 할 수 있다.

다른 사람들이 이미 만들어 놓은 모듈을 사용할 수도 있고 우리가 직접 만들어서 사용할 수도 있다. 

## **모듈 만들기**

모듈에 대해 자세히 살펴보기 전에 간단한 모듈을 한번 만들어 보자.

```python
# mod1.py
def add(a, b):
return a + b

def sub(a, b):
return a-b
```

위와 같이 add와 sub 함수만 있는 파일 mod1.py를 만들고 `C:\doit` 디렉터리에 저장하자.

이 mod1.py 파일이 바로 모듈이다.

> 파이썬 확장자 .py로 만든 파이썬 파일은 모두 모듈이다.
> 

## **모듈 불러오기**

```python
C:\Users\pahkey>cd C:\doit
C:\doit>dir
...
2014-09-23 오후 01:53 49 mod1.py
...
C:\doit>python
>>>
```

```python
>>> import mod1
>>> print(mod1.add(3, 4))
7
>>> print(mod1.sub(4, 2))
2
```

실수로 `import mod1.py`로 입력하지 않도록 주의

> import는 현재 디렉터리에 있는 파일이나 파이썬 라이브러리가 저장된 디렉터리에 있는 모듈만 불러올 수 있다. 파이썬 라이브러리는 파이썬을 설치할 때 자동으로 설치되는 파이썬 모듈을 말한다.
> 

```python
import 모듈이름
```

여기에서 모듈 이름은 mod1.py에서 .py 확장자를 제거한 mod1만을 가리킨다.

때로는 `mod1.add`, `mod1.sub`처럼 쓰지 않고 `add`, `sub`처럼 모듈 이름 없이 함수 이름만 쓰고 싶은 경우도 있을 것이다.

> from 모듈이름 import 모듈함수
> 

```python
>>> from mod1 import add
>>> add(3, 4)
7
```

```python
from mod1 import add, sub
```

```python
from mod1 import *
```

07장에서 공부할 정규 표현식에서 `*` 문자는 "모든 것"이라는 뜻인데 파이썬에서도 마찬가지 의미로 사용한다.

따라서 `from mod1 import *`는 mod1 모듈의 모든 함수를 불러와 사용하겠다는 뜻이다.

## **if __name__ == "__main__": 의 의미**

```python
# mod1.py
def add(a, b):
return a+b
def sub(a, b):
return a-b

print(add(1, 4))
print(sub(4, 2))
```

`add(1, 4)`와 `sub(4, 2)`의 결과를 출력하는 문장을 추가했다.

그리고 출력한 결괏값을 확인하기 위해 mod1.py 파일을 다음과 같이 실행해 보자.

```python
C:\doit>python mod1.py
5
2
```

그런데 이 mod1.py 파일의 add와 sub 함수를 사용하기 위해 mod1 모듈을 import할 때는 좀 이상한 문제가 생긴다.

```python
C:\Users\pahkey> cd C:\doit
C:\doit> python
Type "help", "copyright", "credits" or "license" for more information.
>>> import mod1
5
2
```

단지 mod1.py 파일의 add와 sub 함수만 사용하려고 했는데

import mod1을 수행하는 순간 mod1.py 파일이 실행되어 결괏값을 출력한다.

이러한 문제를 방지하려면 mod1.py 파일을 다음처럼 변경해야 한다.

```python
# mod1.py
def add(a, b):
return a+b

def sub(a, b):
return a-b

if __name__ == "__main__":
		print(add(1, 4))
    print(sub(4, 2))
```

`if __name__ == "__main__"`을 사용하면 `C:\doit>python mod1.py`처럼 직접 이 파일을 실행했을 때는 if문 다음 문장이 수행된다.

반대로 대화형 인터프리터나 다른 파일에서 이 모듈을 불러서 사용할 때는 `__name__ == "__main__"`이 거짓이 되어 if문 다음 문장이 수행되지 않는다.

**`__name__` 변수란?**

`__name__` 변수는 파이썬이 내부적으로 사용하는 특별한 변수 이름이다.

만약 `C:\doit>python mod1.py`처럼 직접 mod1.py 파일을 실행할 경우 mod1.py의 `__name__` 변수에는 `__main__` 값이 저장된다. 

하지만 파이썬 셸이나 다른 파이썬 모듈에서 mod1을 import 할 경우에는 mod1.py의 `__name__` 변수에는 mod1.py의 모듈 이름 값 mod1이 저장된다.

`>>> **import** mod1
>>> mod1.__name__
'mod1'`

## **클래스나 변수 등을 포함한 모듈**

지금까지 살펴본 모듈은 함수만 포함했지만 클래스나 변수 등을 포함할 수도 있다. 다음 프로그램을 작성해 보자.

```python
# mod2.py
PI = 3.141592

class Math:
def solv(self, r):
return PI * (r ** 2)

def add(a, b):
return a+b
```

```python
C:\Users\pahkey> cd C:\doit
C:\doit> python
Type "help", "copyright", "credits"or "license"for more information.
>>> import mod2
>>> print(mod2.PI)
3.141592
```

```python
>>> a = mod2.Math()
>>> print(a.solv(2))
12.566368
```

```python
>>> print(mod2.add(mod2.PI, 4.4))
7.541592
```

## **다른 파일에서 모듈 불러오기**

지금까지는 만들어 놓은 모듈 파일을 사용하기 위해 대화형 인터프리터만 사용했다. 이번에는 다른 파이썬 파일에서 이전에 만들어 놓은 모듈을 불러와서 사용하는 방법에 대해 알아보자. 여기에서는 조금 전에 만든 모듈인 mod2.py 파일을 다른 파이썬 파일에서 불러와 사용할 것이다.

먼저 에디터로 `C:\doit\modtest.py` 파일을 다음과 같이 작성하자.

```python
# modtest.py
import mod2
result = mod2.add(3, 4)
print(result)
```

위에서 볼 수 있듯이 다른 파이썬 파일에서도 `import mod2`로 mod2 모듈을 불러와서 사용할 수 있다. 대화형 인터프리터에서 한 것과 마찬가지 방법이다. 위 예제가 정상적으로 실행되기 위해서는 modtest.py 파일과 mod2.py 파일이 동일한 디렉터리(`C:\doit`)에 있어야 한다.

## **모듈을 불러오는 또 다른 방법**

이번에는 모듈을 저장한 디렉터리로 이동하지 않고 모듈을 불러와서 사용하는 방법에 대해 알아보자.

```python
C:\Users\pahkey>cd C:\doit
C:\doit>mkdir mymod
C:\doit>move mod2.py mymod
        1개 파일을 이동했습니다.
```

**sys.path.append 사용하기**

```python
C:\doit>python
>>> import sys
```

이 sys 모듈을 사용하면 파이썬 라이브러리가 설치되어 있는 디렉터리를 확인할 수 있다.

```python
>>> sys.path
['', 'C:\\Windows\\SYSTEM32\\python311.zip', 'c:\\Python311\\DLLs',
'c:\\Python311\\lib', 'c:\\Python311', 'c:\\Python311\\lib\\site-packages']
```

`sys.path`는 파이썬 라이브러리가 설치되어 있는 디렉터리를 보여 준다. 

만약 파이썬 모듈이 위 디렉터리에 들어 있다면 모듈이 저장된 디렉터리로 이동할 필요 없이 바로 불러서 사용할 수 있다. 

`sys.path`에 `C:\doit\mymod` 디렉터리를 추가하면 아무 곳에서나 불러 사용할 수 있다.

sys.path는 리스트이므로 우리는 다음과 같이 할 수 있다.

```python
>>> sys.path.append("C:/doit/mymod")
>>> sys.path
['', 'C:\\Windows\\SYSTEM32\\python311.zip', 'c:\\Python311\\DLLs',
'c:\\Python311\\lib', 'c:\\Python311', 'c:\\Python311\\lib\\site-packages',
'C:/doit/mymod']
>>>
```

sys.path.append를 사용해서 `C:/doit/mymod`라는 디렉터리를 sys.path에 추가했다. 

```python
>>> import mod2
>>> print(mod2.add(3,4))
7
```

### **PYTHONPATH 환경 변수 사용하기**

```python
C:\doit>set PYTHONPATH=C:\doit\mymod
C:\doit>python
>>> import mod2
>>> print(mod2.add(3,4))
7
```

> 맥이나 유닉스 환경에서는 set 대신 export 명령을 사용해야 한다.

<br>

출처: 점프 투 파이썬 - 박응용
