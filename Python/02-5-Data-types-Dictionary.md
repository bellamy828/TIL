# 2-5. Dictionary

사람은 누구든지 "이름" = "홍길동", "생일" = "몇 월 며칠" 등으로 나타낼 수 있다.

요즘 사용하는 대부분의 언어도 이러한 대응 관계를 나타내는 자료형을 갖고 있는데,

이를 연관 배열(Associative array) 또는 해시(Hash)라고 한다.

파이썬에서는 이러한 자료형을 Dictionary 라고 하는데,

단어 그대로 해석하면 사전이라는 뜻으로 ,Key와 Value를 한 쌍으로 갖는 자료형이다.

리스트나 튜플처럼 순차적으로(sequential) 해당 요솟값을 구하지 않고 Key를 통해 Value를 얻는다. 

baseball이라는 단어의 뜻을 찾기 위해 사전의 내용을 순차적으로 모두 검색하는 것이 아니라 

baseball이라는 단어가 있는 곳만 펼쳐 보는 것이다.

<br>

## **딕셔너리 생성**

```python
{Key1:Value1, Key2:Value2, Key3:Value3, ...}
```

```python
>>> dic = {'name':'pey', 'phone':'010-9999-1234', 'birth': '1118'}
```

- **딕셔너리 dic의 정보**

| key | value |
| --- | --- |
| name | pey |
| phone | 010-9999-1234 |
| birth | 1118 |

<br>

다음 예는 Key로 정수 값 1, Value로 문자열 'hi'

```python
>>> a = {1: 'hi'}
```

또한 Value에 리스트도 넣을 수 있다.

```python
>>> a = { 'a': [1,2,3]}
```

<br>

## **딕셔너리 쌍 추가, 삭제하기**

### **딕셔너리 쌍 추가하기**

```python
>>> a = {1: 'a'}
>>> a[2] = 'b'
>>> a
{1: 'a', 2: 'b'}
```

```python
>>> a['name'] = 'pey'
>>> a
{1: 'a', 2: 'b', 'name': 'pey'}
```

```python
>>> a[3] = [1,2,3]
>>> a
{1: 'a', 2: 'b', 'name': 'pey', 3: [1, 2, 3]}
```

<br>

### **딕셔너리 요소 삭제하기**

```python
>>>del a[1]
>>> a
{2: 'b', 'name': 'pey', 3: [1, 2, 3]}
```

위 예제는 딕셔너리 요소를 지우는 방법을 보여 준다. 

del 함수를 사용해서 del a[key]처럼 입력하면 지정한 Key에 해당하는 {key : value} 쌍이 삭제된다.

<br>

## **딕셔너리를 사용하는 방법**

### **딕셔너리에서 Key 사용해 Value 얻기**

```python
>>> grade = {'pey': 10, 'julliet': 99}
>>> grade['pey']
10
>>> grade['julliet']
99
```

리스트나 튜플, 문자열은 요솟값을 얻고자 할 때 인덱싱이나 슬라이싱 기법 중 하나를 사용했다. 

하지만 딕셔너리는 Key를 사용해서 Value를 구한다.

위 예에서 'pey'라는 Key의 Value를 얻기 위해 grade['pey']를 사용한 것처럼,

어떤 Key의 Value를 얻기 위해서는 `딕셔너리변수이름[Key]`를 사용한다.

<br>

```python
>>> a = {1:'a', 2:'b'}
>>> a[1]
'a'
>>> a[2]
'b'
```

여기에서 a[1]이 의미하는 것은 리스트나 튜플의 a[1]과는 전혀 다르다.

딕셔너리 변수에서 [ ] 안의 숫자 1은 두 번째 요소를 뜻하는 것이 아니라 Key에 해당하는 1을 나타낸다. 

앞에서도 말했듯이 딕셔너리는 리스트나 튜플에 있는 인덱싱 방법을 적용할 수 없다.

<br>

### **딕셔너리 만들 때 주의할 사항**

딕셔너리에서 Key는 고유한 값이므로 중복되는 Key 값을 설정해 놓으면 하나를 제외한 나머지 것들이 모두 무시된다는 점을 주의해야 한다. 

다음 예에서 볼 수 있듯이 동일한 Key가 2개 존재할 경우 1:'a' 쌍이 무시된다.

```
>>> a = {1:'a', 1:'b'}
>>> a
{1: 'b'}
```

이렇게 Key가 중복되었을 때 1개를 제외한 나머지 Key:Value 값이 모두 무시되는 이유는 

Key를 통해서 Value를 얻는 딕셔너리의 특징에서 비롯된다. 

동일한 Key가 존재하면 어떤 Key에 해당하는 Value를 불러야 할지 알 수 없기 때문이다.

또 한 가지 주의해야 할 사항은 Key에 리스트는 쓸 수 없지만 튜플은 Key로 쓸 수 있다는 것. 

**딕셔너리의 Key로 쓸 수 있느냐 없느냐는 Key가 변하는(mutable) 값인지 변하지 않는(immutable) 값인지에 달려 있다.** 

리스트는 그 값이 변할 수 있기 때문에 Key로 쓸 수 없다. 

다음 예처럼 리스트를 Key로 설정하면 리스트를 키 값으로 사용할 수 없다는 오류가 발생한다.

```python
>>> a = {[1,2] : 'hi'}
Traceback (most recent call last):
  File "<stdin>", line 1,in <module>
TypeError: unhashable type: 'list'
```

단, Value에는 변하는 값이든 변하지 않는 값이든 상관없이 아무 값이나 넣을 수 있다.

<br>

## **딕셔너리 관련 함수들**

딕셔너리를 자유자재로 사용하기 위해 딕셔너리가 자체적으로 가지고 있는 관련 함수를 사용해 보자.

### **Key 리스트 만들기(keys)**

```python
>>> a = {'name': 'pey', 'phone': '010-9999-1234', 'birth': '1118'}
>>> a.keys()
dict_keys(['name', 'phone', 'birth'])
```

a.keys()는 딕셔너리 a의 Key만을 모아서 dict_keys 객체를 리턴한다.

<br>

**파이썬 3.0 이후 버전의 keys 함수**
파이썬 2.7 버전까지는 a.keys() 함수를 호출하면 dict_keys가 아닌 리스트를 리턴.

리스트를 리턴하기 위해서는 메모리 낭비가 발생하는데 파이썬 3.0 이후 버전에서는 이러한 메모리 낭비를 줄이기 위해 dict_keys 객체를 리턴하도록 변경.

다음에 소개할 dict_values, dict_items 역시 파이썬 3.0 이후 버전에서 추가된 것들이다. 

만약 3.0 이후 버전에서 리턴 값으로 리스트가 필요한 경우에는 `list(a.keys())`를 사용하면 된다. dict_keys, dict_values, dict_items 객체는 리스트로 변환하지 않더라도 기본적인 반복 구문(예: for문)에서 사용할 수 있다.

<br>

dict_keys 객체는 다음과 같이 사용할 수 있다. 

리스트를 사용하는 것과 차이가 없지만, 리스트 고유의 append, insert, pop, remove, sort 함수는 수행할 수 없다.

```python
>>>for k in a.keys():
...    print(k)
...
name
phone
birth
```

> print(k)를 입력할 때 들여쓰기를 하지 않으면 오류가 발생하니 주의
> 

dict_keys 객체를 리스트로 변환하려면 다음과 같이 하면 된다.

```python
>>> list(a.keys())
['name', 'phone', 'birth']
```

<br>

### **Value 리스트 만들기(values)**

```python
>>> a.values()
dict_values(['pey', '010-9999-1234', '1118'])
```

<br>

### **Key, Value 쌍 얻기(items)**

```python
>>> a.items()
dict_items([('name', 'pey'), ('phone', '010-9999-1234'), ('birth', '1118')])
```

<br

### **Key: Value 쌍 모두 지우기(clear)**

```python
>>> a.clear()
>>> a
{}
```

clear 함수는 딕셔너리 안의 모든 요소를 삭제한다.

> 빈 리스트를 [], 빈 튜플을 ()로 표현하는 것과 마찬가지로 빈 딕셔너리도 {}로 표현한다.
> 

<br>

### **Key로 Value얻기(get)**

```python
>>> a = {'name':'pey', 'phone':'010-9999-1234', 'birth': '1118'}
>>> a.get('name')
'pey'
>>> a.get('phone')
'010-9999-1234'
```

```python
>>> a = {'name':'pey', 'phone':'010-9999-1234', 'birth': '1118'}
>>> print(a.get('nokey'))
None
>>> print(a['nokey'])
Traceback (most recent call last):
  File "<stdin>", line 1,in <module>
KeyError: 'nokey'
```

앞에서 살펴보았듯이 `a.get('name')`은 `a['name']`을 사용했을 때와 동일한 결괏값을 리턴한다.

다만 다음 예제에서 볼 수 있듯이 `a['nokey']`처럼 딕셔너리에 존재하지 않는 키로 값을 가져오려고 할 경우 

`a['nokey']` 방식은 오류를 발생시키고 `a.get('nokey')` 방식은 None을 리턴한다는 차이가 있다.

<br>

딕셔너리 안에 찾으려는 Key가 없을 경우 미리 정해 둔 디폴트 값을 대신 가져오게 하고 싶을 때에는 **get(x, '디폴트 값')**을 사용

```python
>>> a.get('nokey', 'foo')
'foo'

```

- 딕셔너리 a에는 'nokey'에 해당하는 Key가 없다. 따라서 디폴트 값인 'foo'를 리턴한다.

<br>

### **해당 Key가 딕셔너리 안에 있는지 조사하기(in)**

```python
>>> a = {'name':'pey', 'phone':'010-9999-1234', 'birth': '1118'}
>>> 'name' in a
True
>>> 'email' in a
False
```

<br> 

출처: 점프 투 파이썬 - 박응용
