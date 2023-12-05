# 파이썬 Numpy

## Numpy란?

- Numeric Python의 줄인말입니다.
- 통계나 연산작업시 사용되는 라이브러리입니다.
- 파이썬의 리스트와 흡사하며, 리스트보다 빠르고 메모리 효율성이 높아 성능적인 측면에서 훨씬 우위를 차지한다는 점이 있습니다.
- Import numpy as np 로 사용하면 됩니다.

## Numpy 배열 VS 리스트

- numpy의 array 함수 사용

```python
// 리스트
myList = [1,2,3,4,5]
print(myList) // [1, 2, 3, 4, 5]

// numpy의 array
myArr = np.array(myList)
print(myArr) // [1 2 3 4 5]
```

- Numpy와 리스트 타입 비교

```python
// 리스트 타입 
print(type(myList)) // <class 'list'>

// numpy의 array 타입 
print(type(myArr)) // <class 'numpy.ndarray'> -- ndarray 넘파이 배열, ndarray 클래스 타입
```

- Numpy와 리스트 인덱스 슬라이싱
- 인덱싱: 몇번째인지 가르키는데 사용합니다.
- 슬라이싱: 몇번째 부터인지 또는 몇번째까지 또는 몇번부터 출력하기 위해서 자르기 위해서 사용합니다.

```python
// 리스트
myList_slice = myList[1:3] // 인덱스 슬라이싱 - 1번부터 2번까지 출력
myList_slice[0] = -5

// numpy의 array 타입
myArr_slice = myArr[1:3]
myArr_slice[0] = -5

// 둘의 차이점
- print(myList) // 원본이 변하지 않으며, 복사본을 만든다.
- print(myArr) // 원본을 즉시 바꿔버린다. 그 덕분에 메모리 효율성이 뛰어납니다.
```

## Numpy의 랜덤함수

```python
exRand = np.random.rand(10) // 0부터 1사이의 실수를 랜덤으로 5개의 인덱스를 만들어준다.
print(exRand)

// Tip: ?를 뒤에 사용하면 그에 대한 설명이 나옵니다.
# np.random.rand?

exRandint = np.random.randint(1, 10, 6) // 1부터 10까지의 숫자 6개를 뽑아냅니다.
print(exRandint)

exRandn = np.random.randn(10) // 가우시간 표준분표
print(exRandn)
```

## Numpy 배열의 초기화

- 초기화란?
  - 배열의 생성함과 동시에 최초의 값을 넣는다는 의미입니다.
  - 특정한 값을 할당하는 것을 말합니다.
  - Numpy의 초기화 함수는 다음 종류들이 있습니다.
    - Zeros(): 0의 값으로 이뤄진 크기가 10인 배열을 생성
    - Ones(): 1의 값으로 이뤄진 크기가 10인 배열을 생성
    - Arrange(): 0부터 10까지의 인덱스를 생성합니다. 만약 (3, 9)로 한다면 3부터 9까지 (2, 90, 10) 하면 2부터 90까지 10씩 뛰면서 배열을 생성합니다.
    - Eye(): 1 by 1 단위의 배열을 생성
    - full(): 특정 값만큼 배열을 생성 -- Ex) np.full(크기, 값)

```python
// zeros()
az = np.zeros(10)
print(az)

// ones()
ao = np.ones(10)
print(ao)
print(np.ones(10)+3) // 4의 값으로 이뤄진 크기가 10인 배열을 생성

// eye(3) - 3 by 3 단위의 배열을 생성
ae = np.eye(5)
print(ae)
print('ae + 1 : ', ae[2]*1) // ae + 1 : [0. 0. 1. 0. 0.]
print(ae)

// arrange(10)
print(np.arrange(2, 90, 10))
a = np.arrange(2, 100, 10)
print(a)

// full()
af = np.full((5,5), -11) // np.full(크기, 값)
print(af)
```

## Numpy 배열 과 리스트의 차이점

- 리스트는 서로다른 타입의 값들이 저장이 가능하지만, np 배열(=Numpy 배열)은 하나의 자료형만 저장할 수 있습니다.(단, 더 큰 타입으로 캐스팅 됩니다. int, string이랑 있으면 string이 더 큰 타입이기 때문에 포함됩니다.)

```python
L = [1,2,3,'4',5]
number = [1,2,3,4.6,5]
print(L)
print(type(L))
print(number)

nparray_1 = np.array(L)
print(narray_1)
print(type(narray_1))

narray_2 = np.array(number)
print(narray_2)
print(type(narray_2))

// 값의 타입을 명시해서 저장할 수도 있습니다. 이때에는 dtype라는 속성을 사용하면 됩니다.
narray_3 = np.array([1,2,3,4], dtype = np.float) // 같은 자료형만 저장합니다.
print(narray_3)
```

## Numpy 배열의 속성 or 함수

- ndim: 차원값을 반환
- Shape: 배열의 행과 열
- Reshape: 행과 열을 바꿔줍니다.
- Size: Element 의 갯수
- type: 타입
- Astype(): 배열의 원소값 타입을 한 번에 다른 타입으로 바꿀 수 있습니다.

```python
arr1 = np.array([[1.0, 2, 3], [4, 5, 6]], dtype=np.int32) // 2 by 3 (= 2행 3열) 으로 나옵니다.

// np의 함수를 이용해서 타입, 차원, 몇행몇열, 데이터가 총 몇개인지, 출력

print(type(arr1)) // 타입
print(np.ndim(arr1)) // 2차원: 매트릭스, 1차원: 벡터
print(np.shape(arr1)) // 몇 행 몇 열
print(np.size(arr1)) // Element의 갯수

arr1_1 = arr1.astype(np.float64)
print(arr1_1.dtype)

arr2 = np.arange(32) // 1차원으로 이루어진 배열
print(arr2)
arr2_2 = arr2.reshape(8, 4) // 2차원 구조로 변형
print(arr2_2)
```

## 랜덤함수와 Seed 값 설정하기

- 여러 값을 저장할 땐 시드값으로 설정할 수 있습니다.
- 여러 명이서 작업할 때 랜덤한 값이 나오되, 동일한 랜덤한 값이 나오도록 지정하는 방법입니다.
- 시드값을 설정하지 않을 때에는 랜덤한 값 난수 값이 컴퓨터 시간을 기준으로 그때마다 다른 값이 나오도록 설정되어 있습니다.
- 시드값은 seed() 함수 안에 숫자를 넣음으로써 수동으로 값을 만들어내는 알고리즘
- seed 값은 0 혹은 양의 정수만 가능합니다.

```python
import numpy as np
np.random.seed(0)
```

## 인덱싱과 조건 슬라이싱

- 열거된 배열의 값에서 논리연산자 혹은 where 함수를 사용해서, 내가 원하는 값을 가져올 수 있어야 합니다.

```python
arr2 = np.random.randn(4,4)

// 논리 연산자 사용
arr2[arr<0]

// 0보다 작은 값들(음수)는 전부 다 0으로 바꿔보겠습니다.
arr2[arr2 < 0] = 0
print(arr2) // 원본이 변경되었습니다.

// where 함수 사용
arr2_w = np.where(arr2>0, arr2, -1) // 3항 연산자 arr2 > 0이 true이면 arr2를 반환하고, false이면 -1를 리턴합니다.
print(arr2_w)
```

