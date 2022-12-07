# 2-2.  문자열(String)

파이썬에서 문자열을 만드는 방법은 총 4가지이다.

**1. 큰따옴표(`"`)로 양쪽 둘러싸기**

```
"Hello World"
```

**2. 작은따옴표(`'`)로 양쪽 둘러싸기**

```
'Python is fun'
```

**3. 큰따옴표 3개를 연속(`"""`)으로 써서 양쪽 둘러싸기**

```
"""Life is too short, You need python"""
```

**4. 작은따옴표 3개를 연속(`'''`)으로 써서 양쪽 둘러싸기**

```
'''Life is too short, You need python''
```

<br>

### **문자열 안에 작은따옴표나 큰따옴표를 포함시키고 싶을 때**

**1. 문자열에 작은따옴표 (`'`) 포함시키기**

```
Python's favorite food is perl
```

위와 같은 문자열을 food 변수에 저장하고 싶다고 가정하자. 

문자열 중 Python's에 작은따옴표(')가 포함되어 있다.

이럴 때는 다음과 같이 문자열을 큰따옴표(")로 둘러싸야 한다. 

큰따옴표 안에 들어 있는 작은따옴표는 문자열을 나타내기 위한 기호로 인식되지 않는다.

```
>>> food = "Python's favorite food is perl"
```

```
>>> food
"Python's favorite food is perl"
```

시험 삼아 다음과 같이 큰따옴표(")가 아닌 작은따옴표(')로 문자열을 둘러싼 후 다시 실행해 보자. 

'Python'이 문자열로 인식되어 구문 오류(SyntaxError)가 발생할 것이다.

```python
>>> food = 'Python's favorite food is perl'
  File "<stdin>", line 1
    food = 'Python's favorite food is perl'
                   ^
SyntaxError: invalid syntax

```

<br>

**2. 문자열에 큰따옴표 (`"`) 포함시키기**

```
"Python is very easy." he says.
```

위와 같이 큰따옴표(")가 포함된 문자열이라면 다음과 같이 문자열을 작은따옴표(')로 둘러싸면 된다.

```
>>> say = '"Python is very easy." he says.'
```

<br>

**3. 백슬래시(`\`)를 사용해서 작은따옴표(`'`)와 큰따옴표(`"`)를 문자열에 포함시키기**

```
>>> food = 'Python\'s favorite food is perl'
>>> say = "\"Python is very easy.\" he says."
```

 백슬래시(`\`)를 작은따옴표(')나 큰따옴표(") 앞에 삽입하면 

백슬래시(`\`) 뒤의 작은따옴표(')나 큰따옴표(")는 문자열을 둘러싸는 기호의 의미가 아니라 

문자 ('), (") 그 자체를 뜻하게 된다.

<br>

### **여러 줄인 문자열을 변수에 대입하고 싶을 때**

```
Life is too short
You need python
```

**1. 줄을 바꾸기 위한 이스케이프 코드 `\n` 삽입하기**

```
>>> multiline = "Life is too short\nYou need python"

```

위 예처럼 줄바꿈 문자 `\n`을 삽입하는 방법이 있지만 읽기에 불편하고 줄이 길어지는 단점이 있다.

<br>

**2. 연속된 작은따옴표 3개(`'''`) 또는 큰따옴표 3개(`"""`) 사용하기**

위 1번의 단점을 극복하기 위해 파이썬에서는 다음과 같이 작은따옴표 3개(''') 또는 큰따옴표 3개(""")를 사용한다.

```
>>> multiline='''
... Life is too short
... You need python
... '''

```

*작은따옴표 3개를 사용한 경우*

```
>>> multiline="""
... Life is too short
... You need python
... """

```

*큰따옴표 3개를 사용한 경우*

print(multiline)을 입력해서 어떻게 출력되는지 확인해 보자.

```
>>> print(multiline)
Lifeis too short
You need python

```

<br>

### **이스케이프 코드란?**

문자열 예제에서 여러 줄의 문장을 처리할 때 백슬래시 문자와 소문자 n을 조합한 `\n` 이스케이프 코드를 사용했다. 

이스케이프 코드란 프로그래밍할 때 사용할 수 있도록 미리 정의해 둔 "문자 조합"이다. 

주로 출력물을 보기 좋게 정렬하는 용도로 사용한다. 

<img width="372" alt="image" src="https://user-images.githubusercontent.com/72433598/206212621-2f7af52e-78e2-4a07-b7d0-782530edace3.png">

이중에서 활용빈도가 높은 것은 `\n`, `\t`, `\\`, `\'`, `\"`이다.

<br>

## **문자열 연산하기**

파이썬에서는 문자열을 더하거나 곱할 수 있다. 

### **문자열 더해서 연결하기(Concatenation)**

```
>>> head = "Python"
>>> tail = " is fun!"
>>> head + tail
'Python is fun!'

```

<br>

### **문자열 곱하기**

```
>>> a = "python"
>>> a * 2
'pythonpython'

```

위 소스 코드에서 `*`의 의미는 우리가 일반적으로 사용하는 숫자 곱하기의 의미와는 다르다. 

위 소스 코드에서 `a * 2` 문장은 a를 두 번 반복하라는 뜻이다. 

### **문자열 곱하기 응용**

```
# multistring.py

print("=" * 50)
print("My Program")
print("=" * 50)
```

```
C:\Users>cd C:\doit
C:\doit>python multistring.py
==================================================
My Program
==================================================
```

<br>

### **문자열 길이 구하기**

문자열의 길이는 다음과 같이 len 함수를 사용하면 구할 수 있다. 

len 함수는 print 함수처럼 파이썬의 기본 내장 함수로 별다른 설정 없이 바로 사용할 수 있다.

```
>>> a = "Life is too short"
>>> len(a)
17
```

<br>

## **문자열 인덱싱과 슬라이싱**

### **문자열 인덱싱이란?**

```
>>> a = "Life is too short, You need Python"
```

```
Life is too short, You need Python
0         1         2         3
0123456789012345678901234567890123
```

```
>>> a = "Life is too short, You need Python"
>>> a[3]
'e'
```

<br>

### **문자열 인덱싱 활용하기**

```
>>> a = "Life is too short, You need Python"
>>> a[0]
'L'
>>> a[12]
's'
>>> a[-1]
'n'

```

a[-1]은 뒤에서부터 세어 첫 번째가 되는 문자를 말한다. 

a의 값은 "Life is too short, You need Python" 문자열이므로 

뒤에서부터 첫 번째 문자는 가장 마지막 문자 'n'이다.

```
>>> a[-0]
'L'
```

```
>>> a[-2]
'o'
>>> a[-5]
'y'
```

<br>

### **문자열 슬라이싱이란?**

"Life is too short, You need Python" 문자열에서 'Life' 또는 'You' 같은 단어를 뽑아내기 

다음과 같이 하면 된다.

```
>>> a = "Life is too short, You need Python"
>>> b = a[0] + a[1] + a[2] + a[3]
>>> b
'Life'
```

위 방법처럼 단순하게 접근할 수도 있지만 파이썬에서는 더 좋은 방법을 제공한다. 

> 인덱싱 기법과 슬라이싱 기법은 뒤에서 배울 자료형인 리스트나 튜플에서도 사용할 수 있다.
> 

위 예는 슬라이싱 기법으로 다음과 같이 간단하게 처리할 수 있다.

```
>>> a = "Life is too short, You need Python"
>>> a[0:4]
'Life'
```

a[0:4]가 뜻하는 것은 a 문자열, 즉 "Life is too short, You need Python" 문장에서 자리 번호 0부터 4 바로 앞(3)까지의 문자를 뽑아낸다는 뜻이다. 

```
>>> a[0:3]
'Lif'
```

슬라이싱 기법으로 a[시작 번호:끝 번호]를 지정할 때 끝 번호에 해당하는 것은 포함하지 않는다.

<br>

### **문자열을 슬라이싱하는 방법**

슬라이싱의 예를 조금 더 보자.

```
>>> a[0:5]
'Life '
```

```
>>> a[0:2]
'Li'
>>> a[5:7]
'is'
>>> a[12:17]
'short'
```

a[시작 번호:끝 번호]에서 끝 번호 부분을 생략하면 시작 번호부터 그 문자열의 끝까지 뽑아낸다.

```
>>> a[19:]
'You need Python'
```

a[시작 번호:끝 번호]에서 시작 번호를 생략하면 문자열의 처음부터 끝 번호까지 뽑아낸다.

```
>>> a[:17]
'Life is too short'
```

a[시작 번호:끝 번호]에서 시작 번호와 끝 번호를 생략하면 문자열의 처음부터 끝까지를 뽑아낸다.

```
>>> a[:]
'Life is too short, You need Python'
```

슬라이싱에서도 인덱싱과 마찬가지로 마이너스(-) 기호를 사용할 수 있다.

```
>>> a[19:-7]
'You need'
```

위 소스 코드에서 a[19:-7]이 뜻하는 것은 a[19]에서부터 a[-8]까지를 말한다. 이 역시 a[-7]은 포함하지 않는다.

<br>

### **슬라이싱으로 문자열 나누기**

```
>>> a = "20010331Rainy"
>>> date = a[:8]
>>> weather = a[8:]
>>> date
'20010331'
>>> weather
'Rainy'
```

위 문자열 "20010331Rainy"를 연도 2001, 월과 일을 나타내는 0331, 날씨를 나타내는 Rainy의 세 부분으로 나누려면 다음과 같이 할 수 있다.

```
>>> a = "20010331Rainy"
>>> year = a[:4]
>>> day = a[4:8]
>>> weather = a[8:]
>>> year
'2001'
>>> day
'0331'
>>> weather
'Rainy'
```

**"Pithon"이라는 문자열을 "Python"으로 바꾸려면?**

Pithon 문자열을 Python으로 바꾸려면 어떻게 해야 할까? 제일 먼저 떠오르는 생각은 다음과 같을 것이다.

```
>>> a = "Pithon"
>>> a[1]
'i'
>>> a[1] = 'y'
```

즉 a 변수에 "Pithon" 문자열을 대입하고 a[1]의 값이 i니까 a[1]을 y로 바꾸어 준다는 생각이다. 

하지만 결과는 어떻게 나올까? 당연히 오류가 발생한다. 

왜냐하면 문자열의 요솟값은 바꿀 수 있는 값이 아니기 때문이다(문자열 자료형은 그 요솟값을 변경할 수 없다. 그래서 immutable한 자료형이라고도 부른다).
하지만 앞에서 살펴본 슬라이싱 기법을 사용하면 Pithon 문자열을 사용해 Python 문자열을 만들 수 있다.
다음 예를 보자.

```
>>> a = "Pithon"
>>> a[:1]
'P'
>>> a[2:]
'thon'
>>> a[:1] + 'y' + a[2:]
'Python'
```

위 예에서 볼 수 있듯이 슬라이싱을 사용하면 "Pithon" 문자열을 'P' 부분과 'thon' 부분으로 나눌 수 있기 때문에 그 사이에 'y' 문자를 추가하여 'Python'이라는 새로운 문자열을 만들 수 있다.

<br>

출처: 점프 투 파이썬 01장 파이썬이란 무엇인가? - 박응용
