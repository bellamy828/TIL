# 6-1. os 모듈 활용한 하위 디렉토리 탐색 

특정 디렉터리부터 시작해서 그 하위 모든 파일 중 파이썬 파일(`*.py`)만 출력해 주는 프로그램을 만들려면 어떻게 해야 할까?

**1.** 다음과 같이 sub_dir_search.py 파일을 작성해 보자.

> sub_dir_search.py 파일은 C:\doit 디렉터리에 저장한다.
> 

```python
# C:/doit/sub_dir_search.py

def search(dirname):
    print(dirname)

search("c:/")
```

search 함수를 만들고 시작 디렉터리를 입력받도록 코드를 작성했다.

**2.** 이제 이 디렉터리에 있는 파일을 검색할 수 있도록 소스를 변경해 보자.

```python
# C:/doit/sub_dir_search.py
import os

def search(dirname):
    filenames = os.listdir(dirname)
		for filename in filenames:
        full_filename = os.path.join(dirname, filename)
        print(full_filename)

search("c:/")
```

os.listdir를 사용하면 해당 디렉터리에 있는 파일들의 리스트를 구할 수 있다.

여기에서 구하는 파일 리스트는 파일 이름만 포함되어 있으므로 경로를 포함한 파일 이름을 구하기 위해서는 입력으로 받은 dirname을 앞에 덧붙여 주어야 한다.

os 모듈에는 디렉터리와 파일 이름을 이어 주는 os.path.join 함수가 있으므로 이 함수를 사용하면 디렉터리를 포함한 전체 경로를 쉽게 구할 수 있다.

위 코드를 수행하면 `C:/` 디렉터리에 있는 파일이 다음과 비슷하게 출력될 것이다.

*[디렉토리 출력 예]*

```python
c:/$Recycle.Bin
c:/$WINDOWS.~BT
c:/$Windows.~WS
c:/adb
c:/AMD
c:/android
c:/bootmgr
c:/BOOTNXT
… 생략 …
```

**3.** 이제 `C:/` 디렉터리에 있는 파일들 중 확장자가 .py인 파일만을 출력하도록 코드를 변경해 보자.

```python
# C:/doit/sub_dir_search.py
import os

def search(dirname):
    filenames = os.listdir(dirname)
		for filenamein filenames:
        full_filename = os.path.join(dirname, filename)
				ext = os.path.splitext(full_filename)[-1]
						if ext == '.py':
		            print(full_filename)

search("c:/")
```

파일 이름에서 확장자만 추출하기 위해 os 모듈의 os.path.splitext 함수를 사용하였다.

os.path.splitext는 파일 이름을 **확장자**를 기준으로 두 부분으로 나누어 준다. 

따라서 os.path.splitext(full_filename)[-1]은 해당 파일의 확장자 이름이 된다. 

위 코드는 확장자 이름이 .py인 경우만을 출력하도록 작성했다.

`C:/`디렉터리에 파이썬 파일이 없다면 아무것도 출력되지 않을 것이다.

**4.** 하지만 우리가 원하는 것은 `C:/`디렉터리 바로 밑에 있는 파일뿐만 아니라 그 하위 디렉터리(sub directory)를 포함한 모든 파이썬 파일을 검색하는 것이다.

하위 디렉터리도 검색이 가능하도록 다음과 같이 코드를 변경해야 한다.

```python
# C:/doit/sub_dir_search.py
import os

def search(dirname):
		try:
        filenames = os.listdir(dirname)
				for filename in filenames:
            full_filename = os.path.join(dirname, filename)
						if os.path.isdir(full_filename):
                search(full_filename)
						else:
                ext = os.path.splitext(full_filename)[-1]
								if ext == '.py':
                    print(full_filename)
		except PermissionError:
				pass

search("c:/")
```

try ... except PermissionError로 함수 전체를 감싼 이유는 os.listdir를 수행할 때 권한이 없는 디렉터리에 접근하더라도 프로그램이 오류로 종료되지 않고 그냥 수행되도록 하기 위해서이다.

full_filename이 디렉터리인지 파일인지 구별하기 위하여 os.path.isdir 함수를 사용하였고 디렉터리일 경우 해당 경로를 입력받아 다시 search 함수를 호출하였다.

이렇게 해당 디렉터리의 파일이 디렉터리일 경우 다시 search 함수를 호출해 나가면 (재귀 호출) 해당 디렉터리의 하위 파일을 다시 검색하기 시작하므로 결국 모든 파일들을 검색할 수 있게 된다.

**하위 디렉터리 검색을 쉽게 해주는 os.walk**
os.walk를 사용하면 위에서 작성한 코드를 보다 간편하게 만들 수 있다.

os.walk는 시작 디렉터리부터 시작하여 그 하위 모든 디렉터리를 차례대로 방문하게 해주는 함수이다.

```python
**import** os

**for** (path, dir, files) **in** os.walk("c:/"):
    **for** filename **in** files:
        ext = os.path.splitext(filename)[-1]
        **if** ext == '.py':
            print("%s/%s" % (path, filename))
```

디렉터리와 파일을 검색하는 일반적인 경우라면 os.walk를 사용하는 것을 추천한다.

<br>

출처: 점프 투 파이썬 - 박응용 
