# **1. 파이썬이란?**

파이썬(Python)은 1990년 암스테르담의 귀도 반 로섬(Guido Van Rossum)이 개발한 인터프리터 언어이다. 

귀도는 파이썬이라는 이름을 자신이 좋아하는 코미디 쇼인 "몬티 파이썬의 날아다니는 서커스(Monty Python’s Flying Circus)"에서 따왔다고 한다.

> 인터프리터 언어란 한 줄씩 소스 코드를 해석해서 그때그때 실행해 결과를 바로 확인할 수 있는 언어이다.
> 

파이썬의 사전적 의미는 고대 신화에 나오는 파르나소스 산의 동굴에 살던 큰 뱀을 뜻하며, 

아폴로 신이 델파이에서 파이썬을 퇴치했다는 이야기가 전해지고 있다. 

대부분의 파이썬 책 표지와 아이콘이 뱀 모양으로 그려져 있는 이유가 여기에 있다.

![https://wikidocs.net/images/page/5/pahkey_KRRKrp.png](https://wikidocs.net/images/page/5/pahkey_KRRKrp.png)

<br>

파이썬은 컴퓨터 프로그래밍 교육을 위해 많이 사용하지만, 기업의 실무를 위해서도 많이 사용하는 언어이다. 

그 대표적인 예가 바로 구글이다. 이외에도 많이 알려진 예를 몇 가지 들자면 온라인 사진 공유 서비스 인스타그램(Instagram), 파일 동기화 서비스 드롭박스(Dropbox)등이 있다.

<br>

또한 파이썬 프로그램은 공동 작업과 유지 보수가 매우 쉽고 편하다. 

그 때문에 이미 다른 언어로 작성된 많은 프로그램과 모듈이 파이썬으로 재구성되고 있다.
 
<br>

# **2. 파이썬의 특징**

### **파이썬은 인간다운 언어이다**

프로그래밍이란 인간이 생각하는 것을 컴퓨터에 지시하는 행위라고 할 수 있다. 

앞으로 살펴볼 파이썬 문법에서도 보게 되겠지만, 파이썬은 사람이 생각하는 방식을 그대로 표현할 수 있는 언어이다.

따라서 프로그래머는 굳이 컴퓨터의 사고 체계에 맞추어서 프로그래밍을 하려고 애쓸 필요가 없다. 

다음 소스 코드를 보면 이 말이 쉽게 이해될 것이다.

```
if 4in [1,2,3,4]: print("4가 있습니다")

```

위 예제는 다음처럼 읽을 수 있다.

```
만약 4가 1, 2, 3, 4 중에 있으면 "4가 있습니다"를 출력한다.

```

파이썬은 문법 자체가 아주 쉽고 간결하며 사람의 사고 체계와 매우 닮아 있다. 

유명한 프로그래머인 에릭 레이먼드(Eric Raymond)는 파이썬을 공부한 지 단 하루 만에 자신이 원하는 프로그램을 작성할 수 있었다고 한다.

> 프로그래밍 경험이 조금이라도 있다면 파이썬의 자료형, 함수, 클래스 만드는 법, 라이브러리 및 내장 함수 사용 방법 등을 익히는 데 1주일이면 충분하리라 생각한다.
> 

<br>

### **파이썬은 무료이지만 강력하다**

물론 시스템 프로그래밍이나 하드웨어 제어와 같은 매우 복잡하고 반복 연산이 많은 프로그램은 파이썬과 어울리지 않는다. 

하지만 파이썬은 이러한 약점을 극복할 수 있게끔 다른 언어로 만든 프로그램을 파이썬 프로그램에 포함시킬 수 있다.

파이썬과 C는 찰떡궁합이란 말이 있다. 즉 프로그램의 전반적인 뼈대는 파이썬으로 만들고, 

빠른 실행 속도가 필요한 부분은 C로 만들어서 파이썬 프로그램 안에 포함시키는 것이다.

사실 파이썬 라이브러리 중에는 순수 파이썬만으로 제작된 것도 많지만 C로 만든 것도 많다.

C로 만든 것은 대부분 속도가 빠르다.

> 파이썬 라이브러리는 파이썬 프로그램을 작성할 때 불러와 사용할 수 있는 미리 만들어 놓은 파이썬 파일 모음이다.
> 
  
<br>  

### **파이썬은 간결하다**

귀도는 파이썬을 의도적으로 간결하게 만들었다. 

만약 펄(Perl)과 같은 프로그래밍 언어가 100가지 방법으로 하나의 일을 처리할 수 있다면 파이썬은 가장 좋은 방법 1가지만 사용하는 것을 선호한다. 

이 간결함의 철학은 파이썬 문법에도 그대로 적용되어 파이썬 프로그래밍을 하는 사람들은 잘 정리되어 있는 소스 코드를 볼 수 있다. 

다른 사람이 작업한 소스 코드도 한눈에 들어와 이해하기 쉽기 때문에 공동 작업과 유지 보수가 아주 쉽고 편하다.

다음은 파이썬 프로그램의 예제이다.

```python
# simple.py
languages = ['python', 'perl', 'c', 'java']

for langin languages:
if langin ['python', 'perl']:
        print("%6s need interpreter" % lang)
elif langin ['c', 'java']:
        print("%6s need compiler" % lang)
else:
        print("should not reach here")

```

이 예제는 프로그래밍 언어를 판별하여 그에 맞는 문장을 출력하는 파이썬 프로그램 예제이다. 

다른 언어에서 늘 보게 되는 단락을 구분하는 괄호({ }) 문자가 보이지 않는 것을 확인할 수 있다. 

또한 줄을 참 잘 맞춘 코드라는 것도 알 수 있다. 

파이썬 프로그램은 줄을 맞추지 않으면 실행되지 않는다. 

코드를 예쁘게 작성하려고 줄을 맞추는 것이 아니라 프로그램이 실행되게 하려면 꼭 줄을 맞추어야 하는 것이다. 

이렇듯 줄을 맞추어 코드를 작성하는 행위는 가독성에 크게 도움이 된다.

> 파이썬에서 들여쓰기를 하지 않으면 프로그램이 실행되지 않는다.
> 

<br>

### **파이썬은 개발 속도가 빠르다**

<br>

# **3. 파이썬으로 무엇을 할 수 있을까?**

### **시스템 유틸리티 제작**

파이썬은 운영체제(윈도우, 리눅스 등)의 시스템 명령어를 사용할 수 있는 각종 도구를 갖추고 있기 때문에

이를 바탕으로 갖가지 시스템 유틸리티를 만드는 데 유리하다. 

> 유틸리티란 컴퓨터 사용에 도움을 주는 여러 소프트웨어를 말한다.
> 

<br>

### **GUI 프로그래밍**

GUI(Graphic User Interface) 프로그래밍이란 쉽게 말해 화면에 윈도우 창을 만들고 그 창에 프로그램을 동작시킬 수 있는 메뉴나 버튼 등을 추가하는 것이다. 

파이썬은 GUI 프로그래밍을 위한 도구들이 잘 갖추어져 있어 GUI 프로그램을 만들기 쉽다. 

대표적인 예로 파이썬 프로그램과 함께 설치되는 Tkinter(티케이인터)가 있다. 

Tkinter를 사용하면 단 5줄의 소스 코드만으로 윈도우 창을 띄울 수 있다.

<br>

### **C/C++와의 결합**

파이썬은 접착(glue) 언어라고도 부르는데, 그 이유는 다른 언어와 잘 어울려 결합해서 사용할 수 있기 때문이다.

C나 C++로 만든 프로그램을 파이썬에서 사용할 수 있으며, 파이썬으로 만든 프로그램 역시 C나 C++에서 사용할 수 있다.

<br>

### **웹 프로그래밍**

<br>

### **수치 연산 프로그래밍**

사실 파이썬은 수치 연산 프로그래밍에 적합한 언어는 아니다. 

수치가 복잡하고 연산이 많다면 C 같은 언어로 하는 것이 더 빠르기 때문이다. 

하지만 파이썬은 넘파이(NumPy)라는 수치 연산 모듈을 제공한다. 

이 모듈은 C로 작성했기 때문에 파이썬에서도 수치 연산을 빠르게 할 수 있다.

<br>

### **데이터베이스 프로그래밍**

파이썬은 사이베이스(Sybase), 인포믹스(Infomix), 오라클(Oracle), 마이에스큐엘(MySQL), 포스트그레스큐엘(PostgreSQL) 등의 데이터베이스에 접근하기 위한 도구를 제공한다.

또한 이런 굵직한 데이터베이스를 직접 사용하는 것 외에도 파이썬에는 재미있는 도구가 하나 더 있다. 

바로 피클(pickle)이라는 모듈이다. 피클은 파이썬에서 사용하는 자료를 변형 없이 그대로 파일에 저장하고 불러오는 일을 맡아 한다. 

<br>

### **데이터 분석, 사물 인터넷**

파이썬으로 만든 판다스(Pandas) 모듈을 사용하면 데이터 분석을 더 쉽고 효과적으로 할 수 있다.

데이터 분석을 할 때 아직까지는 데이터 분석에 특화된 "R" 이라는 언어를 많이 사용하고 있지만, 

판다스가 등장한 이후로 파이썬을 사용하는 경우가 점점 증가하고 있다.

사물 인터넷 분야에서도 파이썬은 활용도가 높다. 

한 예로 라즈베리파이(Raspberry Pi)는 리눅스 기반의 아주 작은 컴퓨터이다. 

라즈베리파이를 사용하면 홈시어터나 아주 작은 게임기 등 여러 가지 재미있는 것들을 만들 수 있는데, 

파이썬은 이 라즈베리파이를 제어하는 도구로 사용된다. 

예를 들어 라즈베리파이에 연결된 모터를 작동시키거나 LED에 불이 들어오게 하는 일을 파이썬으로 할 수 있다.

<br>

### **머신러닝 프로그래밍**

요새 파이썬을 가장 핫한 언어로 떠오르게 만든 장본인은 바로 머신러닝 분야이다.

> 머신러닝(Machine learning)은 인공지능의 하위 분야로 경험을 통해 자동으로 발전하는 컴퓨터 알고리즘을 연구하는 분야이다.
> 

파이썬은 머신러닝 프로그램을 작성하기에 가장 적합한 도구이며,

머신러닝 프로그램 작성을 도와주는 사이킷런(scikit-learn), 텐서플로(Tensorflow), 파이토치(PyTorch), 케라스(Keras) 등의 수 많은 라이브러리들을 사용할 수 있다.

<br>

# **4. 파이썬 기초 문법**

### **사칙연산**

1 **더하기**(+) 2는 3이라는 값을 출력해 보자. 보통 계산기 사용하듯 더하기 기호만 넣어 주면 된다.

```python
>>> 1 + 2
3

```

**나눗셈**(/)과 **곱셈**(`*`) 역시 예상한 대로 결괏값을 보여준다.

```python
>>> 3 / 2.4
1.25
>>> 3 * 9
27

```

우리가 일반적으로 알고 있는 ÷ 기호나 × 기호가 아닌 것에 주의하자.

### **변수에 숫자 대입하고 계산하기**

```python
>>> a = 1
>>> b = 2
>>> a + b
3

```

a에 1을, b에 2를 대입한 다음 a와 b를 더하면 3이라는 결괏값을 보여 준다.

### **변수에 문자 대입하고 출력하기**

```python
>>> a = "Python"
>>> print(a)
Python

```

a 변수에 Python이라는 값을 대입한 다음 print(a)라고 작성하면 a 값을 출력한다.

> 파이썬은 대소문자를 구별한다. print를 PRINT로 쓰면 오류가 발생한다.
> 

또는 다음과 같이 print문을 생략하고 변수 이름 a만 입력하여 a의 값을 확인할 수도 있다.

```python
>>> a = "Python"
>>> a
'Python'

```

<br>

### **조건문 if**

다음은 간단한 조건문 if를 사용한 예제이다.

```python
>>> a = 3
>>>if a > 1:
...     print("a는 1보다 큽니다.")
...
a는 1보다 큽니다.

```

앞의 예제는 a가 1보다 크면 "a는 1보다 큽니다." 라는 문장을 출력(print)하라는 뜻이다. 

위 예제에서 a는 3이므로 1보다 크다.

따라서 두 번째 "..." 이후에 `Enter`키를 입력하면 if문이 종료되고 "a는 1보다 큽니다." 문장이 출력된다.

> print문 앞의 '...'은 아직 문장이 끝나지 않았음을 의미한다.
> 

`if a > 1:` 다음 문장은 `Tab` 키 또는 `Spacebar` 키 4개를 이용해 반드시 들여쓰기 한 후에 

`print("a는 1보다 큽니다.")`라고 작성해야 한다.

들여쓰기 규칙에 대해서는 03장 제어문에서 자세하게 알아볼 것이다. 

바로 뒤에 이어지는 반복문 for, while 예제도 마찬가지로 들여쓰기가 필요하다.

<br>

### **반복문 for**

다음은 **for**를 사용해서 [1, 2, 3] 안의 값을 하나씩 출력하는 것을 보여 주는 예이다.

```python
>>>for ain [1, 2, 3]:
...     print(a)
...
1
2
3

```

for문을 사용하면 실행해야 할 문장을 여러 번 반복해서 실행시킬 수 있다. 

위 예는 대괄호([ ])사이에 있는 값들을 하나씩 출력한다. 

위 코드의 의미는 "[1, 2, 3] 리스트의 앞에서부터 하나씩 꺼내어 a 변수에 대입한 후

`print(a)`를 수행하라"이다.

당연히 a에 차례로 1, 2, 3이라는 값이 대입되며 `print(a)`에 의해서 그 값이 차례대로 출력된다.

<br>

### **반복문 while**

다음은 **while**을 사용하는 예이다.

```python
>>> i = 0
>>>while i < 3:
...     i=i+1
...     print(i)
...
1
2
3

```

while이라는 영어 단어는 "~인 동안"이란 뜻이다. 

for문과 마찬가지로 반복해서 문장을 수행할 수 있도록 해준다. 

위 예제는 i 값이 3보다 작은 동안 `i=i+1`과 `print(i)`를 수행하라는 말이다. 

`i=i+1`이라는 문장은 i의 값을 1씩 더하게 한다. 

i 값이 3보다 커지게 되면 while문을 빠져나가게 된다.

<br>

### **함수**

파이썬의 **함수**는 다음과 같은 형태이다.

```python
>>>def add(a, b):
...return a+b
...
>>> add(3,4)
7

```

파이썬에서 def는 함수를 만들 때 사용하는 예약어이다. 

위 예제는 add 함수를 만들고 그 함수를 어떻게 사용하는지를 보여준다. 

add(a, b)에서 a, b는 입력값이고, a+b는 결괏값이다. 

즉 3, 4가 입력으로 들어오면 3+4를 수행하고 그 결괏값인 7을 리턴한다.

> 예약어란 프로그래밍 언어에서 이미 문법적인 용도로 사용하고 있는 단어를 말한다. 리턴(return)은 함수 실행 후 그 값을 반환하는 행위를 말한다.

<br><br>


출처: 점프 투 파이썬 - 박응용 
