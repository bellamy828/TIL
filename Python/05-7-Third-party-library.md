# 5-7. 외부 라이브러리 

## **pip**

pip은 파이썬 모듈이나 패키지를 쉽게 설치할 수 있도록 도와주는 도구

pip으로 파이썬 프로그램을 설치하면 의존성 있는 모듈이나 패키지를 함께 설치해 주기 때문에 매우 편리하다.

예를 들어 B라는 파이썬 패키지를 설치하려면 A라는 패키지가 먼저 설치되어야 하는 규칙이 있다고 할 때 pip을 이용하면 B 패키지를 설치할 때 A 패키지도 자동으로 함께 설치된다.

### **pip install**

PyPI(Python Package Index)는 파이썬 소프트웨어가 모인 저장 공간이다.

이곳에서 직접 내려받아 설치해도 되지만 pip을 이용하면 다음과 같이 간편하게 설치를 할 수 있다.

```python
pip install SomePackage
```

여기서 SomePackage는 내려받을 수 있는 특정 패키지를 뜻한다.

### **pip uninstall**

설치한 패키지를 삭제하고 싶다면 다음의 명령어로 삭제할 수 있다.

```python
pip uninstall SomePackage
```

### **특정 버전으로 설치하기**

다음과 같이 버전을 지정하여 설치할 수도 있다. 다음 명령어를 실행하면 1.0.4 버전의 SomePackage를 설치한다.

```python
pip install SomePackage==1.0.4
```

다음처럼 버전을 생략하면 최신 버전을 설치한다.

```python
pip install SomePackage
```

### **최신 버전으로 업그레이드하기**

패키지를 최신 버전으로 업그레이드하려면 --upgrade 옵션과 함께 사용한다.

```python
pip install --upgrade SomePackage
```

### **설치된 패키지 확인하기**

다음 명령은 pip을 이용하여 설치한 패키지 목록을 출력한다.

```python
pip list
```

다음과 같이 설치된 패키지 목록을 출력할 것이다.

```python
Package                  Version
------------------------ --------
amqp                     2.1.4
anyjson                  0.3.3
billiard                 3.3.0.23
celery                   3.1.0
defusedxml               0.4.1
diff-match-patch         20121119
(... 생략 ...)
```

## **Faker**

이번에는 pip을 사용하여 유용한 외부 라이브러리중 하나인 faker를 설치하고 사용해 보자.

faker는 테스트용 가짜 데이터를 생성할 때 사용하는 라이브러리이다.

faker 라이브러리는 pip을 이용하여 설치해야 한다.

```python
C:\> pip install Faker
```

### **Faker 사용해 보기**

만약 다음과 같은 형식의 테스트 데이터 30건이 필요하다고 가정

```python
[(이름1, 주소1), (이름2, 주소2), ..., (이름30, 주소30)]
```

테스트 데이터는 faker를 사용하면 아주 쉽게 만들 수 있다. 이름은 다음처럼 만들 수 있다.

```python
>>> from faker import Faker
>>> fake = Faker()
>>> fake.name()
'Matthew Estrada'
```

한글 이름이 필요하다면 다음과 같이 한국을 의미하는 ko-KR을 전달하여 fake 객체를 생성하면 된다.

```python
>>> fake = Faker('ko-KR')
>>> fake.name()
'김하은'
```

주소는 다음과 같이 만들 수 있다.

```python
>>> fake.address()
'경기도 수원시 경수대로'
```

따라서 이름과 주소를 쌍으로 하는 30건의 테스트 데이터는 다음과 같이 만들 수 있다.

```python
>>> test_data = [(fake.name(), fake.address()) for i in range(30)]
```

```python
>>> test_data
[('이예진', '인천광역시 동대문구 언주거리 (경자김면)'), ('윤도윤', '광주광역시 서초구 삼성로 (주원최박리)'), ('서동현', '인천광역시 관악구 잠실가 (민석엄김마을)'), ('김광수', '울산광역시 양천구 서초대로'), ('이예은', '광주광역시 성북구 개포522길'), ('김병철', '전라북도 춘천시 양재천52로 (현숙김읍)'), ('임서윤', '제주특별자치도 증평군 봉은사3로 (지민이윤리)'), ('김지연', '충청북도 의정부시 학동64가'), ('나지혜', '대구광역시 북구 도산대717거리'), ('박하은', '서울특별시 성동구  서초중앙길'), ('김영환', '부산광역시 성북구 강남대52가'), ('이은주', '대구광역시 동대문구 도산대로'), ('지서현', '전라남도 보령시 잠실0가 (미영김마을)'), ('김예은', '인천광역시 관악구 삼성길'), ('김현정', '강원도 금산군 서초대101가'), ('김 영자', '전라남도 부천시 소사구 압구정로 (미영이면)'), ('김예원', '충청남도 안양시 동안구 가락5로 (예은이읍)'), ('이지후', '경상북도 부천시 테헤란길'), ('김민준', '대구광역시 노원구 서초대가'), ('이상호', '광주광역시 강서구 삼성6로'), ('박보람', '울산광역시 강서구 석촌호수606길 (성진이조읍)'), ('이하은', '전라남도 서천군 선릉거리'), ('박미영', '경상남도 파주 시 삼성로 (병철안이동)'), ('황병철', '강원도 청주시 청원구 영동대1길 (하윤손리)'), ('김영순', '충청남도 안양시 동안구 반포대가 (수진배동)'), ('박성현', '전라남도 서산시 가락27길 (준영박문읍)'), ('김성호', '경상남도 영월군 학동거리'), ('백지우', '경기도 계룡시 서초대1로'), ('권유진', '경기도 양주시 서초중앙313가 (춘자나리)'), ('윤서준', '경상남도 청주시 서원 구 서초대64가')]
```

### **Faker 활용**

faker는 앞서 살펴본 name, address 이외에 다른 항목도 제공한다.

| 항목 | 설명 |
| --- | --- |
| fake.name() | 이름 |
| fake.address() | 주소 |
| fake.postcode() | 우편 번호 |
| fake.country() | 국가명 |
| fake.company() | 회사명 |
| fake.job() | 직업명 |
| fake.phone_number() | 휴대 전화 번호 |
| fake.email() | 이메일 주소 |
| fake.user_name() | 사용자명 |
| fake.pyint(min_value=0, max_value=100) | 0부터 100 사이의 임의의 숫자 |
| fake.ipv4_private() | IP 주소 |
| fake.text() | 임의의 문장 (한글 임의의 문장은 fake.catch_phrase() 사용) |
| fake.color_name() | 색상명 |

## **sympy**

sympy는 방정식 기호(symbol)를 사용하게 해주는 외부 라이브러리이다.

```python
C:\> pip install sympy
```

### **sympy 사용해 보기**

시윤이는 가진 돈의 2/5로 학용품을 샀다고 한다.

이때 학용품을 사는 데 쓴 돈이 1,760원이라면 남은 돈은 어떻게 구하면 될까?

이 문제는 연습장과 연필만 있으면 쉽게 구할 수 있는 일차방정식 문제이다.

파이썬으로는 다음처럼 sympy를 사용하면 방정식을 쉽게 풀 수 있다.

먼저 다음과 같이 fractions 모듈과 sympy 모듈이 필요하다.

```python
>>> from fractions import Fraction
>>> import sympy
```

시윤이가 가진 돈을 x라 하면 sympy 모듈을 사용하여 다음과 같이 표현할 수 있다.

```python
>>> x = sympy.symbols("x")
```

sympy.symbols()는 x처럼 방정식에 사용하는 미지수를 나타내는 기호를 생성할 때 사용한다.

**여러개의 기호 사용하기**
x, y 두 개의 미지수가 필요하다면

```python
x, y = sympy.symbols('x y')
```

시윤이가 가진 돈의 2/5가 1,760원, 즉 일차방정식 x∗(2/5)=1760

```python
>>> f = sympy.Eq(x*Fraction('2/5'), 1760)
```

sympy.Eq(a, b)는 a와 b가 같다는 방정식이다.

여기서 사용한 Fraction은 유리수를 표현할 때 사용하는 파이썬 클래스로, 2/5를 정확하게 계산하고자 사용했다.

**fractions.Fraction**
파이썬에서 유리수 연산을 정확하게 하려면 fractions.Fraction을 사용해야 한다.

```python
>>> **from** fractions **import** Fraction
```

유리수는 다음처럼 Fraction(분자, 분모) 형태로 만들 수 있다.

```python
>>> a = Fraction(2, 5)
>>> a
Fraction(2, 5)
```

또는 다음과 같이 Fraction('분자/분모')처럼 문자열로 만들 수도 있다.

```python
>>> a = Fraction('2/5')
>>> a
Fraction(2, 5)
```

f라는 방정식을 세웠으므로 sympy.solve(f)로 x에 해당하는 값을 구할 수 있다.

```python
>>> result = sympy.solve(f)
>>> result
[4400]
```

방정식의 해는 여러 개일 수 있으므로 solve() 함수는 결괏값으로 리스트를 리턴한다. 

결과를 보면 시윤이가 원래 가진 돈이 4,400원임을 알 수 있다. 

따라서 남은 돈은 다음처럼 가진 돈에서 1,760원을 빼면 된다.

```python
>>> remains = result[0] - 1760
>>> remains
2640
```

종합 풀이

```python
from fractionsimport Fraction
import sympy

# 가지고 있던 돈을 x라고 하자.
x = sympy.symbols("x")

# 가지고 있던 돈의 2/5가 1760원이므로 방정식은 x * (2/5) = 1760 이다.
f = sympy.Eq(x*Fraction('2/5'), 1760)

# 방정식을 만족하는 값(result)을 구한다.
result = sympy.solve(f)  # 결괏값은 리스트

# 남은 돈은 다음과 같이 가지고 있던 돈에서 1760원을 빼면 된다.
remains = result[0] - 1760

print('남은 돈은 {}원 입니다.'.format(remains))
```

### **sympy 활용**

x^2=1과 같은 이차방정식의 해를 구해보자.

```python
>>> import sympy
>>> x = sympy.symbols("x")
>>> f = sympy.Eq(x**2, 1)
>>> sympy.solve(f)
[-1, 1]
```

또한, 다음과 같은 연립방정식의 해도 구할 수 있다.

```python
x + y = 10
x - y = 4
```

```python
>>> import sympy
>>> x, y = sympy.symbols('x y')
>>> f1 = sympy.Eq(x+y, 10)
>>> f2 = sympy.Eq(x-y, 4)
>>> sympy.solve([f1, f2])
{x: 7, y: 3}
```

미지수가 2개 이상이라면 결괏값이 리스트가 아닌 딕셔너리

<br>

출처: 점프 투 파이썬 - 박응용
