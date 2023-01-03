# 7-1. 유니코드

컴퓨터는 0과 1이라는 값만 인식할 수 있는 기계 장치이다.  
이런 컴퓨터가 문자를 인식하려면 어떻게 해야 할까? 과거부터 지금까지 사용하는 유일한 방법은 다음과 비슷한 방법으로 문자 셋을 만드는 것이다.  

예를 들어 숫자 48은 'a', 숫자 49는 'b', … 이런 식으로 숫자마다 문자를 매핑해 놓으면 컴퓨터는 해당 숫자를 문자로 대체하여 인식할 수 있을 것이다.  
최초 컴퓨터가 발명되었을 때 이런 문자를 처리하고자 컴퓨터마다 각각의 문자셋을 정해 놓고 문자를 처리하기 시작했다.  
하지만, 이렇게 컴퓨터마다 각각의 문자셋을 사용했더니 데이터 호환이 안 되는 문제가 발생했다. A 컴퓨터에서 처리하는 문자셋 규칙이 B 컴퓨터에서 처리하는 문자셋 규칙과 같지 않기 때문에 서로 데이터를 주고받는 등의 일을 할 수가 없었던 것이다.  

이런 문제를 해결하고자 미국에서 최초 문자셋 표준인 아스키(ASCII)가 탄생하게 된다.  
아스키라는 문자셋 규칙을 정하고 이 규칙대로만 문자를 만들면 다른 기종 컴퓨터 간에도 문제없이 데이터를 주고받을 수 있었다.  
아스키는 처리할 수 있는 문자 개수가 127개였는데, 영어권 국가에서 사용하는 영문자, 숫자 등을 처리하는 데는 부족함이 없었다.  
하지만, 곧 비영어권 국가에서도 자신의 문자를 컴퓨터로 표현하고자 하는 요구가 생겼다.  
아스키는 127개의 문자만을 다룰 수 있으므로 아스키를 사용할 수는 없는 노릇이었다.  
그래서 곧 서유럽 문자셋인 ISO8859가 등장하게 되고 한국에서는 KSC5601과 같은 문자셋이 등장하게 된다.  

이렇게 나라마다 문자셋이 만들어지고 또 한 나라에서도 여러 개의 문자셋이 표준이 되고자 치열한 싸움을 벌이기도 하며 문자를 처리하는 방법은 점점 더 복잡해져만 갔다.  
가장 결정적인 문제는 하나의 문서에 여러 나라의 언어를 동시에 표현할 방법이 없다는 점이었다.  

이런 문제를 해결하고자 등장한 것이 바로 유니코드(Unicode)이다.  
유니코드는 모든 나라의 문자를 다 포함하게끔 넉넉하게 설계되었고 곧 세계 표준으로 자리 잡게 되었다.  

## **인코딩**

다음과 같은 문자열을 보자.

```python
>>> a = "Life is too short"
```

파이썬에서 사용하는 문자열은 모두 유니코드 문자열이다. (파이썬 3 버전부터 모든 문자열을 유니코드로 처리하도록 변경되었다.)

유니코드 문자열은 **인코딩**(encoding) 없이 그대로 파일에 적거나 다른 시스템으로 전송할 수 없다.

왜냐하면 유니코드 문자열은 단순히 문자셋의 **규칙**이기 때문이다.

파일에 적거나 다른 시스템으로 전송하려면 바이트로 변환해야 한다.

이렇게 유니코드 문자열을 바이트로 바꾸는 것을 인코딩이라 한다.

따라서 파일을 읽거나 네트워크를 통해 바이트 문자열을 수신할 때에는 해당 바이트가 어떤 방식의 인코딩을 사용했는지를 미리 알아야만 디코딩할 수 있다.

유니코드 문자열을 바이트 문자열로 바꾸는 방법은 다음과 같다.

```python
>>> a = "Life is too short"
>>> b = a.encode('utf-8')
>>> b
b'Life is too short'
>>> type(b)
<class 'bytes'>
```

유니코드 문자열을 바이트 문자열로 만들 때에는 이 예처럼 `utf-8`과 같은 인코딩 방식을 인수로 넘겨 주어야 한다.

인수를 생략하면 기본값인 `utf-8`로 동작한다.

문자열을 변환하고 나서 type 명령어를 호출해 보면 b 객체는 bytes 클래스의 객체임을 알 수 있다.

이번에는 다음 예제를 보자.

```python
>>> a = "한글"
>>> a.encode("ascii")
Traceback (most recent call last):
  File "<stdin>", line 1,in <module>
UnicodeEncodeError: 'ascii' codec can't encode characters in position 0-1: ordinal not in range(128)
```

이 예에서는 한글이라는 유니코드 문자열을 아스키(ascii) 방식으로 인코딩하려고 시도한다.

하지만, 아스키 방식으로는 한글을 표현할 수 없으므로 오류가 발생한다.

"한글"이라는 유니코드 문자열을 바이트로 변경하는 인코딩 방식에는 여러 개가 있다.

보통은 utf-8을 사용하지만, 기존 시스템이 euc-kr과 같은 인코딩을 사용한다면 다음과 같이 euc-kr로 인코딩할 수도 있다.

```python
>>> a = '한글'
>>> a.encode('euc-kr')
b'\xc7\xd1\xb1\xdb'
>>> a.encode('utf-8')
b'\xed\x95\x9c\xea\xb8\x80'
```

utf-8로 인코딩 했을 때와는 다른 바이트 문자열을 출력하는 것을 확인할 수 있다.

## **디코딩**

이번에는 반대로 인코딩한 바이트 문자열을 유니코드 문자열로 변환하는 디코딩(decoding)을 알아보자.

다음 예제처럼 euc-kr로 인코딩한 바이트 문자열은 euc-kr로만 디코딩해야 한다.

```python
>>> a = '한글'
>>> b = a.encode('euc-kr')
>>> b.decode('euc-kr')
'한글'
```

이와는 달리 euc-kr로 인코딩한 바이트 문자열을 utf-8로 디코딩하려 한다면 어떻게 될까?

```python
>>> b.decode('utf-8')
Traceback (most recent call last):
  File "<stdin>", line 1,in <module>
UnicodeDecodeError: 'utf-8' codec can't decode byte 0xc7 in position 0: invalid continuation byte
```

잘못된 인코딩 방식으로 디코딩하려 하면 이처럼 오류가 발생한다.

## **입출력과 인코딩**

인코딩과 관련해서 개발자가 가장 고생하는 부분은 바로 데이터 입출력 관련이다.

이것 역시 문자열과 인코딩에 대한 개념만 확실히 이해하면 어렵지 않지만, 

이를 이해하지 못하고 무작정 인코딩, 디코딩을 사용하면 다중 인코딩되거나 문자열이 꼬이게 됨

파일을 읽거나 네트워크를 통해 데이터를 주고받을 때 추천하는 방법은 다음과 같다.

1. 입력으로 받은 바이트 문자열은 가능한 한 가장 빨리 유니코드 문자열로 디코딩할 것
2. 유니코드 문자열만 함수나 클래스 등에서 사용할 것
3. 입력에 대한 결과를 전송하는 마지막 부분에서만 유니코드 문자열을 바이트 문자열로 인코딩해서 반환할 것

이와 같은 규칙을 지킨다면 인코딩과 관련해서 큰 어려움은 없을 것이다.

다음은 euc-kr 방식으로 작성한 파일을 읽고 변경하여 저장하는 예제이다.

```python
# 1. euc-kr로 작성된 파일 읽기
with open('euc_kr.txt', encoding='euc-kr')as f:
    data = f.read()  # 유니코드 문자열

# 2. unicode 문자열로 프로그램 수행하기
data = data + "\n" + "추가 문자열"

# 3. euc-kr로 수정된 문자열 저장하기
with open('euc_kr.txt', encoding='euc-kr', mode='w')as f:
    f.write(data)
```

파일을 읽는 open() 함수에는 encoding을 지정하여 파일을 읽는 기능이 있다.

이때 읽은 문자열은 유니코드 문자열이 된다. 마찬가지로 파일을 만들 때도 encoding을 지정할 수 있다.

encoding 항목을 생략하면 기본값으로 utf-8이 지정된다.

## **소스코드의 인코딩**

파이썬 셸이 아닌 편집기로 코딩할 때는 소스 코드의 인코딩이 매우 중요하다.

소스 코드의 인코딩이란 소스 코드 파일이 현재 어떤 방식으로 인코딩되었지를 뜻한다.

앞의 예제에서 알아보았듯이 파일은 utf-8 인코딩으로 저장할 수도 있고 euc-kr로 저장할 수도 있다.

소스 코드도 파일이므로 인코딩 타입이 반드시 필요하다.

파이썬은 소스 코드의 인코딩을 명시하고자 소스 코드 가장 위에 다음과 같은 문장을 넣어야 한다.

```python
# -*- coding: utf-8 -*-
```

> 파이썬 3.0부터는 utf-8이 기본값이므로 utf-8로 인코딩한 소스 코드라면 이 문장은 생략해도 된다.
> 

소스 코드를 utf-8로 인코딩한 파일이라면 이처럼 작성하면 되고 euc-kr로 인코딩했다면 다음과 같이 작성해야 한다.

```python
# -*- coding: euc-kr -*-
```

소스 코드는 euc-kr로 인코딩했는데 파일 위에 utf-8로 명시했다면 문자열 처리 부분에서 인코딩 관련 오류가 발생할수 있다.

<br>

출처: 점프 투 파이썬 - 박응용
