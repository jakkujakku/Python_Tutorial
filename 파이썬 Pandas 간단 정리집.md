# Pandas 

## Pandas란?

- 데이터프레임을 처리하기 위한 Python의 라이브러리 입니다.
- 데이터프레임이란?
  - 행과 열의 인덱스가 존재하고 인덱스에 맞게 데이터들이 존재하는 데이터구조입니다.
- Series란?
  - 인덱스와 값으로 나타내어지는 열이 '하나'인 자료형은 따로 series 자료형이라고 부릅니다.
  
  

## 데이터프레임 생성

### 1. 라이브러리 부르기

- import pandas as pd 를 사용하여 import 해서 사용하면 됩니다.

### 2. 데이터프레임 '직접' 만들기

- 데이터프레임을 구성하는 요소는 다음 3가지 입니다.
  - 행
  - 열
  - 데이터
- 행 과 열 이름은 생략할 수 있으며, 생략 시 순서에 기번한 정수로 인덱싱됩니다.

```python
import pandas as pd
// syntax
df = pd.dataFrame(data, index, columns)

// 설명
// df : 데이터프레임 이름
// index : 열 이름 L, K
// columns : 행 이름 L, K
```

### 리스트로 만들기

- 1차원 리스트 : 1개 열을 가진 데이터프레임이 생성됩니다.
- 2차원 리스트 : 안쪽에 중첩되어 있는 리스트가 행으로 생성됩니다.

```python
# 2차원 리스트 만들기
2_dim_array = [[1, 2, 3, 4],
         [5, 6, 7, 8],
         [9, 10, 11, 12],
         [13, 14, 15, 16],
         [17, 18, 19, 20]]

# 데이터프레임 만들기
df = pd.DataFrame(2_dim_array)

# 확인
df
```

### 딕셔너리로 만들기

- Key 와 value 로 구성되어 있으므로, key 가 rownames 이 되고, value 가 data 가 됩니다.

### CSV 파일 읽기

- CSV 파일이란? : Comma Seperated Values - 쉼표로 값을 구분한 데이터를 의미한다.

```python
// 읽어오기
df = pd.read_csv(path)
```

- 주요 Parameter

  - Path : 데이터 경로 : 데이터를 읽어올 경로
  - Sep : 구분자를 지정(기본값 : 콤마)
  - Header : 헤더가 될 행 번호(기본값: 0)
  - Index_col : 행 인덱스가 될 열을 지정(기본값: false)
  - Names : 열 이름 지정
  - endoing : 인코딩 방식

  

  ## 데이터프레임

  ### 데이터 확인하는 메서드 or 속성

  #### 상위, 하위 데이터

  - Head(n), tail(n) 메서드 
    - n 에는 정수가 들어가며 확인할 데이터의 갯수를 지정 가능합니다.
    - 기본값은 5입니다.

  #### 데이터 크기

  - Shape 속성
    - (행갯수, 열갯수)의 tuple 형태로 데이터를 반환해줍니다.
    - 행갯수, 열갯수를 따로따로 알고 싶다면 [0], [1] 등 인덱싱을 해주면 됩니다.

  ```python
  # 행만 확인하고 싶다면?
  df.shape[0]
  
  # 열만 확인하고 싶다면?
  df.shape[1]
  ```

  ### 행, 열 정보

  - index 속성
    - 인덱스의 갯수를 알려줍니다.
  - values 속성
    - 행과 열을 제외한 값들을 전부 표시해줍니다. 데이터를 행별로 묶은 2차원 list로 반환해줍니다.
  - colunms 속성
    - 열의 값들과 데이터 타입을 표시해줍니다.

  ### 자료형 확인

  - dtypes 속성
    - 열의 자료형을 알려줍니다.
    - 문자열 데이터는 str 대신 **object** 라고 표현해줍니다.
  - Info() 메서드
    - 열별 자료형, 데이터 갯수, 열의 자료형별 갯수, 메모리 사용량 등을 알려줍니다.

  ### 기술 통계

  - Describe() 메서드
    - 데이터의 기술 통계(Descriptive Statics)를 나타내줍니다.
  - Count: 갯수
  - Mean: 평균
  - Std : 표준편차
  - 25%, 50%, 75%: 사분위 값
  - Max: 최댓값

  - Describe().T : 행과 열을 뒤집어서 보여줍니다.

  

  ## 데이터프레임 조회하기

  ### 데이터 정렬

  - Sort_values()
    - 특정 열을 기준으로 정렬할 수 있습니다.

  ```python
  df.sort_values(by, ascending, inplace)
  ```

  - Df : 데이터프레임 이름
  - by : 기준으로 삼을 열 이름
  - ascending
    - 기본값 - True
    - True 입력하면, 오름차순
    - False 입력하면, 내림차순
  - Inlace : 반영여부
  - List : 복합적으로 정렬 가능

  ### 데이터 집계

  #### 고유값과 최빈값 확인

  - Unique() : 특정 열의 고유값들을 배열로 반환해줍니다.

    ```python
    df[rowname].unique()
    ```

  - Nunique() : 특정 열의 고유값의 개수를 int 로 반환합니다.

    ```python
    df[rowname].nunique()
    ```

  - Value_counts() : 특정 열의 고유값과, 갯수를 series 형태로 반환 해줍니다.

    - Dropna 옵션을 false 로 지정하면 결측치(NaN 값)도 카운트해줍니다.
    - 기본값은 True 입니다.

    ```python
    # 고유값이 2개 이상인 자료들 확인하기
    df[rowname].value_counts(dropna).loc[lamda x : x>1]
    
    # mode() 메서드
    df[rowname].mode()
    # 지정한 열에서의 주어진 값들 중 가장 자주 관측되는 값을 최빈값이라고 합니다.
    # 단, 관측횟수가 같은 경우도 있기 때문에 유일한 값이 아닐 수도 있기 때문에 주의가 필요합니다.
    ```

  #### 기본 통계

  ```python
  df.x(axis)
  ```

  - Df : 데이터명
    - 특정 열(들), 행(들)이 될 수도 있고, 데이터프레임 전체가 될 수도 있습니다.
  - Axis : 축, 입력값으로 0과 1이 있습니다.
    - 0이 행, 1이 열인데 조금 혼동될 수 있는 부분이 있습니다.
    - Axis = 0 을 입력하면, 세로로 집계됩니다.
    - Axis = 1 을 입력하면, 가로로 집계됩니다.
  - x 통계 메서드들
    - Sum() : 합
    - Max() : 최댓값
    - Min() : 최솟값
    - Mean() : 평균값
    - Median() : 중앙값
    - Count() : 갯수
    - Value_counts() : 고유값

  ### 행, 열 조회

  - 행과 열을 조회할 때에는 기본적으로 **df.loc[row, column]** 형태로 조회합니다.
  - iloc 를 이용해서 열을 조회할 수 있습니다.
  - 얇은 코드가 원래 형태입니다.
  - 굵게 표시된 코드 형태가 일반적인 조회 형태입니다.

  <img src="https://velog.velcdn.com/images/dalbong_97/post/db24526b-17b4-4e51-a339-36a5f1941297/image.png">

### 문자열이 포함된 데이터 조회

- Object 로 된 데이터들을 대상으로 .str.contains() 메서드를 이용하여 특정 문자열이 포함된 데이터들을 조회할 수 있습니다.
- 'str' 부분에 조회하고 싶은 문자열을 작성하면 됩니다.

```python
df[df['column_name'].str.contains('str')]
```

