7-3. 이터레이터와 제너레이터

## **이터레이터란?**

이터레이터는 next() 함수 호출 시 계속 그다음 값을 리턴하는 객체이다.

```python
>>> a = [1, 2, 3]
>>> next(a)
Traceback (most recent call last):
  File "<stdin>", line 1,in <module>
TypeError: 'list' object is not an iterator
```

a라는 리스트로 next() 함수를 호출했더니 리스트는 이터레이터 객체가 아니라는 오류가 발생한다. 

즉, 반복 가능하다고 해서 이터레이터는 아니라는 말이다. 

하지만, 반복 가능하다면 다음과 같이 iter() 함수를 이용하여 이터레이터로 만들 수 있다.

```python
>>> a = [1, 2, 3]
>>> ia =iter(a)
>>> type(ia)
<class 'list_iterator'>
```

이제 리스트를 이터레이터로 변경했으므로 next() 함수를 호출해 보자.

```python
>>> next(ia)
1
>>> next(ia)
2
>>> next(ia)
3
>>> next(ia)
Traceback (most recent call last):
  File "<stdin>", line 1,in <module>
StopIteration
```

next() 함수를 호출할 때마다 이터레이터 객체의 요소를 차례대로 리턴하는 것을 확인할 수 있다. 

하지만, 더는 리턴할 값이 없다면 StopIteration 예외가 발생한다. 

이터레이터의 값을 가져오는 가장 일반적인 방법은 다음과 같이 for문을 이용하는 것이다.

```python
>>> a = [1, 2, 3]
>>> ia = iter(a)
>>> for i in ia:
...     print(i)
...
1
2
3
```

```python
>>> a = [1, 2, 3]
>>> ia = iter(a)
>>> for i in ia:
...     print(i)
...
1
2
3
>>> for i in ia:
...     print(i)
...
>>>
```

이처럼 이터레이터는 for문을 이용하여 반복하고 난 후에는 다시 반복하더라도 더는 그 값을 가져오지 못한다. 

next()로 그 값을 한 번 읽으면 그 값을 다시는 읽을 수 없다는 특징이 있다.

## **이터레이터 만들기**

이번에는 iter() 함수를 이용하지 말고 직접 이터레이터를 만드는 방법을 알아보자.

이터레이터는 클래스에 `__iter__`와 `__next__`라는 두 개의 메서드를 구현하면 만들 수 있다.

```python
class MyIterator:
def __init__(self, data):
        self.data = data
        self.position = 0

def __iter__(self):
		return self

def __next__(self):
		if self.position >= len(self.data):
						raise StopIteration
    result = self.data[self.position]
    self.position += 1
		return result

if __name__ == "__main__":
    i = MyItertor([1,2,3])
		for item in i:
        print(item)
```

MyIterator 클래스에는 이터레이터 객체를 생성하고자 `__iter__` 메서드와 `__next__` 메서드를 구현하였다. 

`__iter__` 메서드는 이터레이터 객체를 리턴하는 메서드이므로 MyIterator 클래스에 의해 생성되는 객체를 의미하는 self를 리턴하도록 했다. 

`__next__` 메서드는 next() 함수 호출 시 수행되므로 MyIterator 객체 생성 시 전달한 데이터를 하나씩 리턴하도록 하고 더는 리턴할 값이 없으면 StopIteration 예외를 발생시키도록 구현했다.

이번에는 입력받은 데이터를 역순으로 출력하는 ReverseIterator 클래스를 만들어 보면

```python
class ReverseItertor:
		def __init__(self, data):
        self.data = data
        self.position = len(self.data) -1

		def __iter__(self):
				return self

		def __next__(self):
				if self.position < 0:
						raise StopIteration
        result = self.data[self.position]
        self.position -= 1
				return result

if __name__ == "__main__":
    i = ReverseItertor([1,2,3])
		for item in i:
	        print(item)
```

## **제너레이터란?**

보통 함수는 하나의 값을 리턴했지만 

연속된 값을 차례대로 리턴하는 **제너레이터**(generator) 함수도 있다. 

이터레이터와 마찬가지로 next() 함수 호출 시 그 값을 차례대로 얻을 수 있다. 

이때 **차례대로 결과를 리턴하고자 return 대신 yield 키워드를 사용**한다. 

```python
>>> def mygen():
...     yield 'a'
...     yield 'b'
...     yield 'c'
...
>>> g = mygen()
```

mygen() 함수는 yield 구문을 포함하므로 제너레이터이다. 

제너레이터 객체는 `g = mygen()`과 같이 제너레이터 함수를 호출하여 만들 수 있다. 

type 명령어로 확인하면 g 객체는 제너레이터 타입의 객체임을 알 수 있다. 

```python
>>> type(g)
<class 'generator'>
```

이제 다음과 같이 제너레이터의 값을 차례대로 얻어 보자. 

```python
>>> next(g)
'a'
```

이처럼 제너레이터 객체 g로 next() 함수를 실행하면 mygen() 함수의 첫 번째 yield 문에 따라 'a' 값을 리턴한다. 

여기서 재밌는 점은 제너레이터는 yield라는 문장을 만나면 그 값을 리턴하되 현재 상태를 그대로 기억한다는 점이다. 

이건 마치 음악을 재생하다가 일시 정지 버튼으로 멈춘 것과 비슷한 모양새이다. 

이러한 방식을 전문 용어로 **코루틴**(coroutine)이라 하는데, 이런 이유로 제너레이터를 코루틴이라 부르기도 한다.

```python
>>> next(g)
'b'
```

이번에는 두 번째 yield문에 따라 'b' 값을 리턴한다. 

계속해서 next() 함수를 호출하면 다음과 같은 결과가 출력될 것이다.

```python
>>> next(g)
'c'
>>> next(g)
Traceback (most recent call last):
  File "<stdin>", line 1,in <module>
StopIteration
```

mygen() 함수에는 총 3개의 yield문이 있으므로 4번째 next()를 호출할 때는 더는 리턴할 값이 없으므로 StopIteration 예외가 발생한다.

> 모든 제너레이터는 이터레이터를 만들므로 제너레이터 객체는 이터레이터라 할 수 있다.
> 

## **제너레이터 표현식**

```python
def mygen():
		for i in range(1, 1000):
        result = i * i
				yield result

gen = mygen()

print(next(gen))
print(next(gen))
print(next(gen))
```

mygen() 함수는 1부터 1,000까지 각각의 숫자를 제곱한 값을 순서대로 리턴하는 제너레이터이다.

이 예제를 실행하면 총 3번의 next()를 호출하므로 다음과 같은 결과가 나올 것이다.

```python
1
4
9
```

제너레이터는 def를 이용한 함수로 만들 수 있지만, 다음과 같이 튜플 표현식으로 좀 더 간단하게 만들 수도 있다.

```python
gen = (i * i for i in range(1, 1000))
```

이 표현식은 mygen() 함수로 만든 제너레이터와 완전히 똑같이 기능한다. 

여기서 사용한 표현식은 리스트 컴프리헨션(list comprehension) 구문과 비슷하다. 

다만 리스트 대신 튜플을 이용한 점이 다르다. 

이와 같은 표현식을 **제너레이터 표현식**(generator expression)이라 부른다. 

## **제너레이터와 이터레이터**

지금까지 살펴본 제너레이터는 이터레이터와 서로 상당히 비슷하다는 것을 알 수 있다. 

클래스를 이용하여 이터레이터를 작성하면 좀 더 복잡한 행동을 하게 할 수 있다. 

이와는 달리 제너레이터 표현식 등을 이용하면 간단하게 이터레이터를 만들 수 있다. 

따라서 이터레이터의 성격에 따라 클래스로 만들 것인지 제너레이터로 만들 것인지를 선택해야 한다. 

간단한 경우라면 제너레이터 함수나 제너레이터 표현식을 사용하는 것이 가독성이나 유지보수 측면에서 유리하다. 

다음은 `(i * i for i in range(1, 1000))` 제너레이터를 이터레이터 클래스로 구현한 예이다. 

```python
class MyIterator:
		def __init__(self):
        self.data = 1

		def __iter__(self):
				return self

		def __next__(self):
        result = self.data * self.data
        self.data += 1
				if self.data >= 1000:
						raise StopIteration
				return result
```

이렇게 간단한 경우라면 이터레이터 클래스보다는 제너레이터 표현식을 사용하는 것이 훨씬 간편하고 이해하기 쉽다. 

## **제너레이터의 쓰임새**

제너레이터의 가장 큰 이점은 대량의 데이터를 처리할 때 드러난다는 점을 생각하면 된다. 

다음은 파일을 한 줄씩 읽어서 처리하는 예제이다.

```python
with open('bigdata.txt') as f:
for line in f:
        # process the line
```

파이썬은 기본적으로 파일 객체를 제너레이터로 만들어 처리한다. 

이렇게 제너레이터를 사용하면 파일을 모두 읽어서 메모리에 올려 놓은 후에 처리하는 것이 아니라 한 줄씩 순서대로 처리하기 때문에 작은 메모리로도 대용량 파일을 처리할 수 있다. 

```python
import time

def longtime_job():
    print("job start")
    time.sleep(1)
		return "done"

list_job = iter([longtime_job() for i in range(5)])
print(next(list_job))
```

longtime_job()이라는 함수는 총 실행 시간이 1초인 함수이다. 

이 예제는 longtime_job() 함수를 5번 실행하여 리스트에 그 결괏값을 담고 이를 이터레이터로 변경한 후 그 첫 번째 결괏값을 호출하는 예제이다.

```python
job start
job start
job start
job start
job start
done
```

리스트를 만들 때 이미 5개의 함수를 모두 실행하므로 5초의 시간이 소요되고 이와 같은 결과를 출력한다.

이번에는 이 예제에 제너레이터 기법을 도입

```python
import time

def longtime_job():
    print("job start")
    time.sleep(1)
		return "done"

list_job =(longtime_job() for i in range(5))
print(next(list_job))
```

`iter([longtime_job() for i in range(5)])` 코드를 제너레이터 표현식(`(longtime_job() for i in range(5))`)으로 바꾸었을 뿐이다. 

하지만, 실행 시 1초의 시간만 소요되고 출력되는 결과도 전혀 다르다.

```python
job start
done
```

즉, 모든 함수를 한꺼번에 실행하는 것이 아니라 필요할 때만 실행하는 방식으로 바뀌게 된다.

이러한 방식을 '느긋한 계산법(lazy evaluation)'이라 부른다.

<br>

출처: 점프 투 파이썬 - 박응용
