# 8. 정규 표현식

## **정규 표현식은 왜 필요한가?**

다음과 같은 문제가 주어졌다고 가정해 보자.

```
주민등록번호를 포함하고 있는 텍스트가 있다. 
이 텍스트에 포함된 모든 주민등록번호의 뒷자리를 * 문자로 변경해 보자.
```

우선 정규식을 전혀 모르면 다음과 같은 순서로 프로그램을 작성해야 할 것이다.

1. 전체 텍스트를 공백 문자로 나눈다(split).
2. 나뉜 단어가 주민등록번호 형식인지 조사한다.
3. 단어가 주민등록번호 형식이라면 뒷자리를 ``로 변환한다.
4. 나뉜 단어를 다시 조립한다.

이를 구현한 코드는 아마도 다음과 같을 것이다.

```python
data = """
park 800905-1049118
kim  700905-1059119
"""

result = []
for line in data.split("\n"):
    word_result = []
		for word in line.split(" "):
				if len(word) == 14 and word[:6].isdigit()and word[7:].isdigit():
            word = word[:6] + "-" + "*******"
        word_result.append(word)
    result.append(" ".join(word_result))
print("\n".join(result))
```

```
결괏값:
park 800905-*******
kim  700905-*******
```

```python
import re

data = """
park 800905-1049118
kim  700905-1059119
"""

pat = re.compile("(\d{6})[-]\d{7}")
print(pat.sub("\g<1>-*******", data))
```

```python
결괏값:
park 800905-*******
kim  700905-*******
```

## **정규 표현식의 기초, 메타 문자**

> 메타 문자란 원래 그 문자가 가진 뜻이 아닌 특별한 용도로 사용하는 문자를 말한다.
> 

```python
. ^ $ * + ? { } [  \ | ( )
```

정규 표현식에 위 메타 문자를 사용하면 특별한 의미를 갖게 된다.

### **문자 클래스 [ ]**

우리가 가장 먼저 살펴볼 메타 문자는 바로 문자 클래스(character class)인 [ ]이다.

문자 클래스로 만들어진 정규식은 `"[ ] 사이의 문자들과 매치"`라는 의미를 갖는다.

> 문자 클래스를 만드는 메타 문자인 [ ] 사이에는 어떤 문자도 들어갈 수 있다.
> 

즉 정규 표현식이 [abc]라면 이 표현식의 의미는 "a, b, c 중 한 개의 문자와 매치"를 뜻한다.

- "a"는 정규식과 일치하는 문자인 "a"가 있으므로 매치
- "before"는 정규식과 일치하는 문자인 "b"가 있으므로 매치
- "dude"는 정규식과 일치하는 문자인 a, b, c 중 어느 하나도 포함하고 있지 않으므로 매치되지 않음

  

[ ] 안의 두 문자 사이에 하이픈(-)을 사용하면 두 문자 사이의 범위(From - To)를 의미한다.

예를 들어 [a-c]라는 정규 표현식은 [abc]와 동일하고 [0-5]는 [012345]와 동일

- [a-zA-Z] : 알파벳 모두
- [0-9] : 숫자

  

문자 클래스 안에 `^` 메타 문자를 사용할 경우에는 반대(not)라는 의미를 갖는다. 

예를 들어 `[^0-9]`라는 정규 표현식은 숫자가 아닌 문자만 매치된다.

**자주 사용하는 문자 클래스**
• `\d` - 숫자와 매치, [0-9]와 동일
• `\D` - 숫자가 아닌 것과 매치, `[^0-9]`와 동일
• `\s` - whitespace 문자와 매치, `[ \t\n\r\f\v]`와 동일 (맨 앞의 빈 칸은 공백)
• `\S` - whitespace 문자가 아닌 것과 매치, `[^ \t\n\r\f\v]`와 동일
• `\w` - 문자+숫자(alphanumeric)와 매치, `[a-zA-Z0-9_]`와 동일
• `\W` - 문자+숫자(alphanumeric)가 아닌 문자와 매치, `[^a-zA-Z0-9_]`와 동일

  

### **Dot(.)**

정규 표현식의 Dot(.) 메타 문자는 줄바꿈 문자인 `\n`을 제외한 모든 문자와 매치됨을 의미한다.

> re.DOTALL 옵션을 주면 \n 문자와도 매치된다.
> 

```python
a.b
```

> "a + 모든문자 + b"
> 

즉 a와 b라는 문자 사이에 어떤 문자가 들어가도 모두 매치된다는 의미

- "aab"는 가운데 문자 "a"가 모든 문자를 의미하는 `.`과 일치하므로 정규식과 매치된다.
- "a0b"는 가운데 문자 "0"가 모든 문자를 의미하는 `.`과 일치하므로 정규식과 매치된다.
- "abc"는 "a"문자와 "b"문자 사이에 어떤 문자라도 하나는있어야 하는 이 정규식과 일치하지 않으므로 매치되지 않는다.

<br>

```python
a[.]b
```

> "a + Dot(.)문자 + b"
> 

"a.b" 문자열과 매치되고, "a0b" 문자열과는 매치되지 않는다.

> 만약 앞에서 살펴본 문자 클래스([]) 내에 Dot(.) 메타 문자가 사용된다면 문자 . 그대로를 의미한다.
> 

### **반복 (*)**

```python
ca*t
```

`*` 바로 앞에 있는 문자 a가 0부터 거의 무한대로 반복될 수 있다는 의미

> 사실 메모리 제한으로 2억 개 정도만 가능하다고 함
> 

즉 다음과 같은 문자열이 모두 매치된다.

| 정규식 | 문자열 | Match 여부 | 설명 |
| --- | --- | --- | --- |
| ca*t | ct | Yes | "a"가 0번 반복되어 매치 |
| ca*t | cat | Yes | "a"가 0번 이상 반복되어 매치 (1번 반복) |
| ca*t | caaat | Yes | "a"가 0번 이상 반복되어 매치 (3번 반복) |

  

### **반복 (+)**

`+`는 최소 1번 이상 반복될 때 사용한다. 

`*`가 반복 횟수 0부터라면 `+`는 반복 횟수 1부터

```python
ca+t
```

> "c + a(1번 이상 반복) + t"
> 

위 정규식에 대한 매치여부는 다음 표와 같다.

| 정규식 | 문자열 | Match 여부 | 설명 |
| --- | --- | --- | --- |
| ca+t | ct | No | "a"가 0번 반복되어 매치되지 않음 |
| ca+t | cat | Yes | "a"가 1번 이상 반복되어 매치 (1번 반복) |
| ca+t | caaat | Yes | "a"가 1번 이상 반복되어 매치 (3번 반복) |

  

### **반복 ({m,n}, ?)**

- { } 메타 문자를 사용하면 반복 횟수를 고정
    - {m, n} 정규식을 사용하면 반복 횟수가 m부터 n까지 매치할 수 있음
- 또한 m 또는 n을 생략할 수도 있다.
    - 만약 {3,}처럼 사용하면 반복 횟수가 3 이상인 경우이고 {,3}처럼 사용하면 반복 횟수가 3 이하를 의미
    - 생략된 m은 0과 동일하며, 생략된 n은 2억 개 미만 까지 의미

> {1,}은 +와 동일하고, {0,}은 *와 동일하다.
> 

**1.** {m}

```python
ca{2}t
```

> "c + a(반드시 2번 반복) + t"
> 

| 정규식 | 문자열 | Match 여부 | 설명 |
| --- | --- | --- | --- |
| ca{2}t | cat | No | "a"가 1번만 반복되어 매치되지 않음 |
| ca{2}t | caat | Yes | "a"가 2번 반복되어 매치 |

**2.** {m, n}

```python
ca{2,5}t
```

> "c + a(2~5회 반복) + t"
> 

| 정규식 | 문자열 | Match 여부 | 설명 |
| --- | --- | --- | --- |
| ca{2,5}t | cat | No | "a"가 1번만 반복되어 매치되지 않음 |
| ca{2,5}t | caat | Yes | "a"가 2번 반복되어 매치 |
| ca{2,5}t | caaaaat | Yes | "a"가 5번 반복되어 매치 |

**3.** `?`

`{0, 1}` 과 동일

```python
ab?c
```

위 정규식의 의미는 다음과 같다:

> "a + b(있어도 되고 없어도 된다) + c"
> 

위 정규식에 대한 매치여부는 다음 표와 같다.

| 정규식 | 문자열 | Match 여부 | 설명 |
| --- | --- | --- | --- |
| ab?c | abc | Yes | "b"가 1번 사용되어 매치 |
| ab?c | ac | Yes | "b"가 0번 사용되어 매치 |
- `{m, n}` 형태 보다 `*`, `+`, `?` 메타 문자를 사용하는 편이 가독성이 좋음

  

## **파이썬에서 정규 표현식을 지원하는 re 모듈**

파이썬은 정규 표현식을 지원하기 위해 re(regular expression의 약어) 모듈을 제공한다.

```python
>>> import re
>>> p = re.compile('ab*')
```

re.compile을 사용하여 정규 표현식(위 예에서는 `ab*`)을 컴파일한다.

re.compile의 결과로 돌려주는 객체 p(컴파일된 패턴 객체)를 사용하여 그 이후의 작업을 수행할 것이다.

- 정규식을 컴파일할 때 특정 옵션을 주는 것도 가능
- 패턴이란 정규식을 컴파일한 결과

## **정규식을 이용한 문자열 검색**

| Method | 목적 |
| --- | --- |
| match() | 문자열의 처음부터 정규식과 매치되는지 조사한다. |
| search() | 문자열 전체를 검색하여 정규식과 매치되는지 조사한다. |
| findall() | 정규식과 매치되는 모든 문자열(substring)을 리스트로 리턴한다. |
| finditer() | 정규식과 매치되는 모든 문자열(substring)을 반복 가능한 객체로 리턴한다. |

match, search는 정규식과 매치될 때는 match 객체를 리턴하고, 매치되지 않을 때는 None을 리턴한다.

> match 객체란 정규식의 검색 결과로 리턴된 객체를 말한다.
> 

```python
>>> import re
>>> p = re.compile('[a-z]+')
```

### **match**

match 메서드는 **문자열의 처음부터** 정규식과 매치되는지 조사한다.

```python
>>> m = p.match("python")
>>> print(m)
<re.Match object; span=(0, 6), match='python'>
```

"python" 문자열은 `[a-z]+` 정규식에 부합되므로 match 객체를 돌려준다.

```python
>>> m = p.match("3 python")
>>> print(m)
None
```

"3 python" 문자열은 처음에 나오는 문자 3이 정규식 `[a-z]+`에 부합되지 않으므로 None을 돌려준다.

  

match의 결과로 match 객체 또는 None을 리턴하기 때문에 파이썬 정규식 프로그램은 보통 다음과 같은 흐름으로 작성한다.

```python
p = re.compile(정규표현식)
m = p.match('string goes here')
if m:
    print('Match found: ', m.group())
else:
    print('No match')
```

  

### **search**

```python
>>> m = p.search("python")
>>> print(m)
<re.Match object; span=(0, 6), match='python'
```

"python" 문자열에 search 메서드를 수행하면 match 메서드를 수행했을 때와 동일하게 매치된다.

```python
>>> m = p.search("3 python")
>>> print(m)
<re.Match object; span=(2, 8), match='python'>
```

"3 python" 문자열의 첫 번째 문자는 "3"이지만 **search**는 문자열의 처음부터 검색하는 것이 아니라 **문자열 전체를 검색**하기 때문에 "3 " 이후의 "python" 문자열과 매치된다.

이렇듯 match 메서드와 search 메서드는 문자열의 처음부터 검색할지의 여부에 따라 다르게 사용해야 한다.

  

### **findall**

```python
>>> result = p.findall("life is too short")
>>> print(result)
['life', 'is', 'too', 'short']
```

findall은 패턴(`[a-z]+`)과 매치되는 모든 값을 찾아 리스트로 리턴한다.

  

### **finditer**

```python
>>> result = p.finditer("life is too short")
>>> print(result)
<callable_iterator object at 0x01F5E390>
>>> for r in result: print(r)
...
<re.Match object; span=(0, 4), match='life'>
<re.Match object; span=(5, 7), match='is'>
<re.Match object; span=(8, 11), match='too'>
<re.Match object; span=(12, 17), match='short'>
```

finditer는 findall과 동일하지만 그 결과로 반복 가능한 객체(iterator object)를 리턴한다. 

그리고 반복 가능한 객체가 포함하는 각각의 요소는 match 객체이다.

  

## **match 객체의 메서드**

| method | 목적 |
| --- | --- |
| group() | 매치된 문자열을 리턴한다. |
| start() | 매치된 문자열의 시작 위치를 리턴한다. |
| end() | 매치된 문자열의 끝 위치를 리턴한다. |
| span() | 매치된 문자열의 (시작, 끝)에 해당하는 튜플을 리턴한다. |

다음 예로 확인해 보자.

```python
>>> m = p.match("python")
>>> m.group()
'python'
>>> m.start()
0
>>> m.end()
6
>>> m.span()
(0, 6)
```

match 메서드는 항상 문자열의 시작부터 조사하기 때문에 start()의 결괏값은 항상 0

```python
>>> m = p.search("3 python")
>>> m.group()
'python'
>>> m.start()
2
>>> m.end()
8
>>> m.span()
(2, 8)
```

  

**모듈 단위로 수행하기**
지금까지 우리는 `re.compile`을 사용하여 컴파일된 패턴 객체로 그 이후의 작업을 수행했다.

re 모듈은 이것을 보다 축약한 형태로 사용할 수 있는 방법을 제공한다.

```python
>>> p = re.compile('[a-z]+')
>>> m = p.match("python")
```

  
위 코드가 축약된 형태는 다음과 같다.

```python
>>> m = re.match('[a-z]+', "python")
```

위 예처럼 사용하면 컴파일과 match 메서드를 한 번에 수행할 수 있다. 

보통 한 번 만든 패턴 객체를 여러번 사용해야 할 때는 이 방법보다 `re.compile`을 사용하는 것이 편하다.

  

## **컴파일 옵션**

정규식을 컴파일할 때 다음 옵션을 사용할 수 있다.

- DOTALL(S) - `.` 이 줄바꿈 문자를 포함하여 모든 문자와 매치할 수 있도록 한다.
- IGNORECASE(I) - 대소문자에 관계없이 매치할 수 있도록 한다.
- MULTILINE(M) - 여러줄과 매치할 수 있도록 한다. (`^`, `$` 메타문자의 사용과 관계가 있는 옵션이다)
- VERBOSE(X) - verbose 모드를 사용할 수 있도록 한다. (정규식을 보기 편하게 만들수 있고 주석등을 사용할 수 있게된다.)

옵션을 사용할 때는 `re.DOTALL`처럼 전체 옵션 이름을 써도 되고 `re.S`처럼 약어를 써도 된다.

  

### **DOTALL, S**

`.` 메타 문자는 줄바꿈 문자(`\n`)를 제외한 모든 문자와 매치되는 규칙이 있다.

만약 `\n` 문자도 포함하여 매치하고 싶다면 `re.DOTALL` 또는 `re.S` 옵션을 사용해 정규식을 컴파일하면 된다.

```python
>>> import re
>>> p = re.compile('a.b')
>>> m = p.match('a\nb')
>>> print(m)
None
```

`\n` 문자와도 매치되게 하려면 다음과 같이 `re.DOTALL` 옵션을 사용해야 한다.

```python
>>> p = re.compile('a.b', re.DOTALL)
>>> m = p.match('a\nb')
>>> print(m)
<re.Match object; span=(0, 3), match='a\nb'>
```

보통 `re.DOTALL` 옵션은 여러 줄로 이루어진 문자열에서 줄바꿈 문자에 상관없이 검색할 때 많이 사용한다.

  

### **IGNORECASE, I**

`re.IGNORECASE` 또는 `re.I` 옵션은 대소문자 구별 없이 매치를 수행할 때 사용하는 옵션이다.

```python
>>> p = re.compile('[a-z]+', re.I)
>>> p.match('python')
<re.Match object; span=(0, 6), match='python'>
>>> p.match('Python')
<re.Match object; span=(0, 6), match='Python'>
>>> p.match('PYTHON')
<re.Match object; span=(0, 6), match='PYTHON'>
```

`[a-z]+` 정규식은 소문자만을 의미하지만 re.I 옵션으로 대소문자 구별 없이 매치된다.

  

### **MULTILINE, M**

`re.MULTILINE` 또는 `re.M` 옵션은 메타 문자인 `^`, `$`와 연관된 옵션

`^`는 문자열의 처음을 의미하고, `$`는 문자열의 마지막을 의미

예를 들어 정규식이 `^python`인 경우 문자열의 처음은 항상 python으로 시작해야 매치되고, 

만약 정규식이 `python$`이라면 문자열의 마지막은 항상 python으로 끝나야 매치된다는 의미

```python
import re
p = re.compile("^python\s\w+")

data = """python one
life is too short
python two
you need python
python three"""

print(p.findall(data))
```

정규식 `^python\s\w+`은 python이라는 문자열로 시작하고 그 뒤에 whitespace, 

그 뒤에 단어가 와야 한다는 의미이다. 검색할 문자열 data는 여러 줄로 이루어져 있다.

이 스크립트를 실행하면 다음과 같은 결과를 돌려준다.

```python
['python one']
```

`^` 메타 문자에 의해 python이라는 문자열을 사용한 첫 번째 줄만 매치된 것이다.

하지만 `^` 메타 문자를 문자열 전체의 처음이 아니라 각 라인의 처음으로 인식시키고 싶은 경우에

사용할 수 있는 옵션이 바로 `re.MULTILINE` 또는 `re.M`이다.

```python
import re
p = re.compile("^python\s\w+", re.MULTILINE)

data = """python one
life is too short
python two
you need python
python three"""

print(p.findall(data))
```

`re.MULTILINE` 옵션으로 인해 `^` 메타 문자가 문자열 전체가 아닌 각 줄의 처음이라는 의미를 갖게 되었다.

```python
['python one', 'python two', 'python three']
```

  

### **VERBOSE, X**

```python
charref = re.compile(r'&[#](0[0-7]+|[0-9]+|x[0-9a-fA-F]+);')
```

```python
charref = re.compile(r"""
 &[#]                # Start of a numeric entity reference
 (
     0[0-7]+         # Octal form
   | [0-9]+          # Decimal form
   | x[0-9a-fA-F]+   # Hexadecimal form
 )
 ;                   # Trailing semicolon
""", re.VERBOSE)
```

첫 번째와 두 번째 예를 비교해 보면 컴파일된 패턴 객체인 charref는 모두 동일한 역할을 한다.

하지만 정규식이 복잡할 경우 두 번째처럼 주석을 적고 여러 줄로 표현하는 것이 훨씬 가독성이 좋다는 것을 알 수 있다.

`re.VERBOSE` 옵션을 사용하면 문자열에 사용된 whitespace는 컴파일할 때 제거된다(단 [ ] 안에 사용한 whitespace는 제외). 

그리고 줄 단위로 #기호를 사용하여 주석문을 작성할 수 있다.

  

## **백슬래시 문제**

정규 표현식을 파이썬에서 사용할 때 혼란을 주는 요소가 한 가지 있는데, 바로 백슬래시(`\`)이다.

```python
\section
```

이 정규식은 `\s` 문자가 whitespace로 해석되어 의도한 대로 매치가 이루어지지 않는다.

위 표현은 다음과 동일한 의미이다.

```python
[ \t\n\r\f\v]ection
```

  

의도한 대로 매치하고 싶다면 다음과 같이 변경해야 한다.

```python
\\section
```

정규식에서 사용한 `\` 문자가 문자열 자체임을 알려 주기 위해 백슬래시 2개를 사용하여 이스케이프 처리를 해야 한다.

```python
>>> p = re.compile('\\section')
```

그런데 여기에서 또 하나의 문제가 발견된다. 

위처럼 정규식을 만들어서 컴파일하면 실제 파이썬 정규식 엔진에는 파이썬 문자열 리터럴 규칙에 따라 `\\`이 `\`로 변경되어 `\section`이 전달된다.

> 이 문제는 위와 같은 정규식을 파이썬에서 사용할 때만 발생한다(파이썬의 리터럴 규칙). 유닉스의 grep, vi 등에서는 이러한 문제가 없다.
> 

결국 정규식 엔진에 `\\` 문자를 전달하려면 파이썬은 `\\\\`처럼 백슬래시를 4개나 사용해야 한다.

> 정규식 엔진은 정규식을 해석하고 수행하는 모듈이다.
> 

```python
>>> p = re.compile('\\\\section')
```

이러한 문제를 해결하려면 Raw String을 사용해야 한다.

```python
>>> p = re.compile(r'\\section')
```

위와 같이 정규식 문자열 앞에 r 문자를 삽입하면 이 정규식은 Raw String 규칙에 의하여 백슬래시 2개 대신 1개만 써도 2개를 쓴 것과 동일한 의미를 갖게 된다.

> 만약 백슬래시를 사용하지 않는 정규식이라면 r의 유무에 상관없이 동일한 정규식이 될 것이다.

<br>

출처: 점프 투 파이썬 - 박응용
