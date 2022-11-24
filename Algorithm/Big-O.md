> - 알고리즘 효율을 나타내는 수학적 표기법 
> - 시간 & 공간 복잡도를 나타냄
> - 알고리즘의 증가율을 나타냄 
> - 실제 알고리즘 러닝타임을 측정하는 목적이 아닌, 장기적으로 데이터가 증가함에 따라 연산 시간 증가율 예측 목적
> - 입력값의 변화에 따라 연산을 실행할 때, 연산 횟수에 비해 시간이 얼마만큼 걸리는가

### 1. O(1) - constant time

![](https://images.velog.io/images/taeyeong8/post/7ee24673-4e97-4673-a189-44f12728e79d/%E1%84%89%E1%85%B3%E1%84%8F%E1%85%B3%E1%84%85%E1%85%B5%E1%86%AB%E1%84%89%E1%85%A3%E1%86%BA%202021-11-23%2023.34.15.png)

- 입력된 데이터의 크기와 상관없이 항상 일정한 시간이 소요되는 알고리즘
- 데이터가 증가해도 성능에 변화가 없음

<br>

### 2. O(log n)

![](https://images.velog.io/images/taeyeong8/post/1aeab248-7727-4ba6-863e-9799346adf06/%E1%84%89%E1%85%B3%E1%84%8F%E1%85%B3%E1%84%85%E1%85%B5%E1%86%AB%E1%84%89%E1%85%A3%E1%86%BA%202021-11-24%2000.45.24.png)

- 대표적으로 binary search
- O(1) 다음으로 빠른 시간 복잡도
- 데이터가 증가해도 복잡도 증가폭이 크지 않음

<br>

### 3. O(n) - linear time

![](https://images.velog.io/images/taeyeong8/post/15b33348-f079-487f-97ec-6499cec3a102/%E1%84%89%E1%85%B3%E1%84%8F%E1%85%B3%E1%84%85%E1%85%B5%E1%86%AB%E1%84%89%E1%85%A3%E1%86%BA%202021-11-23%2023.36.16.png)

- 입력된 데이터의 크기에 비례해서 연산이 처리되는 시간 또한 같은 비율로 증가함
- 입력값(n)이 1 증가할 때마다 코드의 실행 시간이 1초씩 증가하는 알고리즘과 실행시간이 2초씩 증가하는 알고리즘이 있다고 할 때, <br>
두 알고리즘 모두 O(n)으로 표기
- 입력값이 커지면 커질수록 계수(n 앞에 있는 수)의 의미(영향력)가 점점 퇴색되기 때문에, <br>
같은 비율로 증가하고 있다면 2배가 아닌 5배, 10배로 증가하더라도 O(n)으로 표기

<br>

### 4-1. O(n^2) - quadratic time

![](https://images.velog.io/images/taeyeong8/post/822742af-ea2c-4e2d-9326-ee0c5e1721a0/%E1%84%89%E1%85%B3%E1%84%8F%E1%85%B3%E1%84%85%E1%85%B5%E1%86%AB%E1%84%89%E1%85%A3%E1%86%BA%202021-11-23%2023.47.43.png)

- 이중 반복문과 같이 한 배열의 길이 n만큼 순회하면서, 각 요소에서 n만큼 또 순회<br> ex) 가로 세로 길이를 각각 n으로 갖는 행렬

<br>

### 4-2. O(nm) - quadratic time

![](https://images.velog.io/images/taeyeong8/post/2431c259-042d-4411-9888-678287e7e6c6/%E1%84%89%E1%85%B3%E1%84%8F%E1%85%B3%E1%84%85%E1%85%B5%E1%86%AB%E1%84%89%E1%85%A3%E1%86%BA%202021-11-23%2023.47.43.png)

- n square와 다른점은 m의 데이터 크기에 따라서 </br> n square 보다 복잡도가 증가할 수도 있고 더 낮은 복잡도 일수도 있음

<br>

### 5. O(n^3) - polynomial / cubic time 

![](https://images.velog.io/images/taeyeong8/post/8fcd2420-34bb-40a6-b09b-2ea895beed2e/%E1%84%89%E1%85%B3%E1%84%8F%E1%85%B3%E1%84%85%E1%85%B5%E1%86%AB%E1%84%89%E1%85%A3%E1%86%BA%202021-11-23%2023.59.02.png)

![](https://images.velog.io/images/taeyeong8/post/a259dfc2-cc51-4b52-b79c-fd43e5b68d11/%E1%84%89%E1%85%B3%E1%84%8F%E1%85%B3%E1%84%85%E1%85%B5%E1%86%AB%E1%84%89%E1%85%A3%E1%86%BA%202021-11-24%2000.38.32.png)

- cubic(3차원) 형태
- O(n^2) 보다 복잡도가 가파르게 상승

<br>

### 6. O(2^n) - exponential complexity
####  Big-O 표기법 중 가장 느린 시간 복잡도

```js
function fibonacci(n) {
	if (n <= 1) {
		return 1;
	}
	return fibonacci(n - 1) + fibonacci(n - 2);
}
```

<br>

### 일반적인 코테 시간 복잡도는

- 데이터 n ≤ 1,000,000 -> 예상 시간 복잡도는 O(n) or O (logn)

- n ≤ 10,000일 경우는 -> O(n2)

- n ≤ 500일 경우는 -> O(n3)
