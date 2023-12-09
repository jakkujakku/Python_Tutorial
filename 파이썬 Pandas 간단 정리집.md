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

------

## 데이터프레임 집계

### Groupby()

- Groupie() 메소드를 이용해 데이터를 집계할 수 있습니다.

```python
df.groupby(by, as_index)['colunmName'].x
```

- by : 집계 기준 열

  - List를 이용하여 여러 열을 집계 기준으로 세울 수 있습니다.

- As_index : 집계 기준 인덱스(기본값: false)

  - 집계기준을 인덱스로 사용할지 여부를 설정할 수 있습니다. 
  - True로 설정시 집계 기준열의 값들이 인덱스로 설정됩니다. 
  - False 면 정수 인덱스로 설정됩니다.

- columnName : 집계할 열

  - '집계 기준' 에 따라 집계할 열
  - List 로 여러 열을 집계할 수 있습니다.
  - 집계할 열을 하나만 작성시 series 자료형으로 반환되므로 [] 를 하나 더 작성하여 데이터프레임으로 반환하도록 권장합니다.
  - 생략 가능하며, 생략할 시 모든 열에 대하여 집계합니다.

- x : 통계 메서드들

  - 범주별로 집계한 데이터들을 통계처리 할 수 있습니다.

- Agg() 

  - 여러 열을 다양한 각각의 통계 메소드로 집계할 수 있습니다.

  ```python
  # Example Agg()
  pass = passes.groupby('team1', as_index = False).agg({'passes team1':'sum', 'passes completed team1':'sum'})
  ```

### Pivot_table()

- Group() 메소드와 달리 집계기준을 열과 행으로 설정할 수 있습니다.

```python
df.pivot_table(index, columns, values, aggfunc)
```

- Index : 집계기준(행)
  - 집계기준이 되는 행을 만들 수 있습니다.
- Columns : 집계기준(열)
  - 집계기준이 되는 열을 만들 수 있습니다.
- Values : 집계값
  - 집계 대상이 되는 값입니다.
- Aggfunc : 통계값
  - 집계 대상을 어떤 통계 방법으로 집계할지 정하는 매개변수입니다.

------

## 데이터프레임 시각화

- pandas 에서 기본적으로 제공하는 시각화를 사용하거나 matplotlib 을 사용합니다.

### plot() 

```python
df.plot(kind)
```

- kind 그릴 그래프의 종류를 지정할 수 있습니다.
  - line
  - bar
  - Hist 등등

### matplotlib

```python
import matplotlib.pyplot as plt

# 고해상도 시각화
%config InlineBackend.figure_format = "retina"
```

------

## 데이터프레임 변경

### 열 이름 변경

- Rename() 메서드와 columns 속성을 이용하여 열의 이름을 변경할 수 있습니다.
- columns 속성

```python
df.columns = ['columnName1', 'columnName2', ... ]
```

- 모든 열을 바꾸는 기능이므로 데이터프레임의 모든 열을 작성해야 하며, 변경을 원하지 않는 열은 기존의 이름을 작성하면 됩니다.

- Rename() 메서드

```python
df.rename(columns = {'columnName1': 'columnName2', ... }, inplace)
```

- columnName1 : 기존 열 이름
- columnName2 : 바꿀 열 이름
- 반영을 위해 변수에 할당해주거나 inplace = True 로 해줍니다.

### 열 추가

- 기존 데이터에서 계산된 결괏값을 저장해야 할 경우에 사용됩니다.

#### 오른쪽에 추가하기

```python
df['columnName'] = df['columnName1'] (operator) df['columnName2']
```

- ColumnName : 추가할 열의 이름
- Operator : 계산을 위한 연산자 +, -, /

#### 원하는 위치에 추가하기 - insert() 

```python
df.insert(indexnum, 'columnName', df['column1'] (operator) df['column2'])
```

- Indexnum : 추가할 열의 위치(int 값), 해당하는 인덱스의 앞에 열이 추가됩니다.

### 행, 열 삭제

- Drop() 메소드를 사용하여 삭제할 수 있습니다.

```python
df.drop(delete, axis, inplace)
```

- delete : 삭제할 행 또는 열
  - 열 이름이 들어갈 수도 있고, 행 또는 열의 인덱스 번호가 들어갈 수도 있습니다.
  - List 를 이용하여 한번에 여러 개를 삭제할 수 있습니다.
- axis : 삭제할 축, 기본값 = 0
  - 행을 삭제할지 열을 삭제할지 정해야 합니다. 0은 행을 삭제하고, 1은 열을 삭제합니다.
- inplace : True 를 입력해 반영해주어야 합니다.

### 인덱스 재설정

- Set_index() 메소드를 이용하여 기존 열을 인덱스로 설정할 수 있습니다.

```python
df.set_index('col', inplace)
```

- Col : 인덱스로 설정할 열 이름
- Inplace : True 를 입력해 반영해주어야 합니다.
- 열 이름이 인덱스의 이름으로 적용됩니다.
- 사용하지 않을 때에는 df.index.name = None 로 삭제해주면 됩니다.
- Reset_index() 메소드를 이용하여 행번호에 기반한 정수값으로 인덱스를 초기화 할 수 있습니다.

```python
df.reset_index(drop)
```

- Drop : 이전 인덱스 버림 여부
  - 인덱스를 초기화 하기 전에 기존에 있던 인덱스를 버릴지 말지 선택하는 옵션입니다.
  - 기본값은 False 이며, 인덱스를 일반 열로 가져옵니다. 
  - True 시 버립니다.
  - 기존의 인덱스를 일반 열로 가져왔을 때(drop = False) 가져온 열의 이름은 index가 되니 rename() 메소드를 이용해 바꿔줍니다.

### multi index 삭제

- Droplevel() 메소드를 이용하여 지울 수 있습니다.
- 예시코드

```python
# Creating a sample MultiIndex DataFrame with multi-indexed columns
data = {('A', 'Sub1'): [1, 2, 3, 4], ('A', 'Sub2'): [5, 6, 7, 8], ('B', 'Sub1'): [9, 10, 11, 12], ('B', 'Sub2'): [13, 14, 15, 16]}
index = pd.Index(['Row1', 'Row2', 'Row3', 'Row4'], name='Index')
columns = pd.MultiIndex.from_tuples([('A', 'Sub1'), ('A', 'Sub2'), ('B', 'Sub1'), ('B', 'Sub2')], names=['Category', 'Subcategory'])
df = pd.DataFrame(data, index=index, columns=columns)

print("Original DataFrame:")
print(df)
print("\n")

# Dropping the 'Subcategory' level from the columns
df_dropped = df.copy()
df_dropped.columns = df_dropped.columns.droplevel('Subcategory')

print("DataFrame after dropping 'Subcategory' level:")
print(df_dropped)
```

- 결과 값(=실행 값)

```python
Original DataFrame:
Category       A         B     
Subcategory Sub1 Sub2 Sub1 Sub2
Index                          
Row1           1    5    9   13
Row2           2    6   10   14
Row3           3    7   11   15
Row4           4    8   12   16


DataFrame after dropping 'Subcategory' level:
Category  A  A   B   B
Index                 
Row1      1  5   9  13
Row2      2  6  10  14
Row3      3  7  11  15
Row4      4  8  12  16
```

### 범주값 변경(매핑)

- Map() 메서드와 replace() 메서드를 이용하면 범주형 값을 다른 값으로 바꿀 수 있습니다.

```python
df.x({ value1: value2 })
```

- x : map or replace
- value1 : 교체 대상
- Value2 : 교체 값

- Map() : 매핑되지 못한 값들을 NaN 값으로 변경
- Replace() : 매핑되지 못한 값들을 그대로 냅둡니다. 전체 프레임 대상으로 매핑이 가능합니다.

### 범주값 만들기(데이터 이산화)

- 이산화(Discretizatin) : 연속 값을 범주값으로 표현하는 과정
- pd.cut() 와 pd.cut() 함수를 이용하여 범주값을 만들 수 있습니다.

- Pd.cut() 함수
  - 데이터의 크기를 기준으로 구간을 나누고 싶을 때 사용합니다.

```python
import pandas as pd
pd.cut(df[column], bins. labels)

# Example
bin = [-np.inf, 2.0, 2.9, 3.5625, np.inf]
tip['gruop'] = pd.cut(df['score'], bins = bin, labels = list('abcd'))
```

- Bins : 나눌 구간
  - int 혹은 int 로 이루어진 list가 들어갑니다.
  - int 를 넣은 경우 범위를 자동으로 나누어 줍니다. (최댓값 - 최솟값/n) 으로 추정합니다.
- Labels : 범위의 이름
  - List 로 나타냅니다.
- Pd.qcut() 함수
  - 갯수를 기준으로 구간을 나눌 때 사용합니다.
  - 구간의 갯수를 지정하면 자동으로 동일한 갯수를 갖는 구간을 만들어줍니다.

```python
import pandas as pd
pd.qcut(df[column], bins, labels)
```

- Bins : 나눌 구간의 '갯수'
  - Int 값만 들어갈 수 있습니다.
- 만약, bins가 4인 경우 4분위수를 기준으로 구간을 나눈 것과 같은 결과가 나옵니다. 즉, cut() 함수에서도 4분위수를 기준으로 구간을 입력하면 같은 결과를 확인할 수 있습니다.

### 자료형 변경

- 날짜 자료형
  - CSV 파일에서 날짜 자료형을 가진 데이터는 object 로 읽어오게 됩니다.
  - Pd.to_datetime() 함수를 이용하면, 날짜 자료형으로 변경할 수 있습니다.

```python
import pandas as pd
pd.to_datetime(df['column'])
```

- 괄호 안에 자료형을 바꾸고 싶은 데이터프레임의 열을 지정하면 됩니다.
- 날짜 자료형인 열에서 다음과 같은 메서드를 이용하면 년과 월을 추출 할 수 있습니다.
  - .dt.year
  - .dt.month
  - .dt.day
  - .dt.time
  - .dt.date
  - .dt.dayofweek

- 다른 자료형
  - 날짜를 제외한 다른 자료형들은 astype() 메서드를 이용하면 다른 자료형으로 변경할 수 있습니다.

```python
df['column'].astype(type)
# or
df.astype({'column'}; 'type')
```

- Type : 원하는 자료형
- Syntax : Str이 들어가는 장소
- to_numeric() 함수 : int or float 로 지정 없이 변경할 수 있습니다.

### 중복값 제거하기

- Value_counts() : 중복값을 집계
- Drop_duplicates() : 집계된 데이터에서 중복값 제거

```python
df.drop_duplicates(inplace, keep, subset)
```

- Inlace : 반영여부
  - 메소드이므로 반영하기 위해서는 True 를 해주어야 합니다.
- Keep : 남길 데이터 (기본값 : keep = first)
  - 중복된 데이터 중 남길 데이터를 선택할 수 있는 옵션입니다.
  - 'first' : 첫번째 데이터를 남깁니다.
  - 'last' : 마지막 데이터를 남깁니다.
  - False : 다 지웁니다.
- Subset : 삭제기준이 될 열
  - 해당 열의 데이터가 같으면, 데이터가 제거됩니다.
  - 열 이름을 str 로 쓰거나, 열의 index 를 작성하면 됩니다.
  - 작성하지 않으면, 해당 행(row)의 데이터가 모두 같아야 제거됩니다.

### 데이터 슬라이싱

- 데이터가 object 자료형인 경우, .str.slice() 메서드를 이용하여 슬라이싱이 가능합니다.

```python
df['column'].str.slice(start, stop)
```

- Start : 슬라이싱을 시작할 인덱스, Int 값입니다.
- Stop : 슬라이싱을 끝낼 인덱스, int 값입니다.
- Range() 함수와 유사하게 끝나 값 -1 까지 카운트 됩니다.

------

## 결측치 처리하기

### 결측치 확인

- Into()
  - 인덱스의 갯수와 null 이 아닌 자료형의 갯수를 알려주므로 두 값에 차이로 결측치 존재 여부와 갯수를 구할 수 있습니다.
- Is null(), not null() 메서드 이용
  - Is null() 메서드
    - 결측치가 있는 데이터를 True 로 나타내며, 없는 곳은 False 로 나타냅니다.
    - isna() 메서드도 같은 기능을 합니다.
  - notnull() 메서드
    - 결측치가 없는 데이터를 True 로 나타내며, 없는 곳은 False 로 나타냅니다.
    - notna() 메서드도 같은 기능을 합니다.
- Sum() 를 사용하면 결측치의 갯수를 구할 수 있습니다.

```python
# Example
air.isna().sum()
```

- 결과 값

```python
Ozone      37
Solar.R     7
Wind        0
Temp        0
Month       0
Day         0
dtype: int64
```

### 결측치 제거

- Drop() 메서드로 결측치가 있는 행이나 열을 제거할 수 있습니다.

```python
df.dropna(subset, axis, inplace)

# Example, Ozone 열이 결측치인 행 제거
air_text.dropna(subset=['Ozone'], axis=0, inplace=True)
```

- Subset : 범위
  - 열 이름을 지정할 수 있습니다.
  - 지정한 열의 결측치만 제거할 수 있습니다.
  - 생략 시, 모든 데이터프레임에 대하여 결측치를 제거합니다.
- axis : 행 또는 열
  - 0 이면 행
  - 1 이면 열
- inplace : 반영 여부
  - 데이터프레임에 변경된 결과를 적용시키려면 True 로 입력해야 합니다.

### 결측치 채우기

#### fillna()

- 결측치를 다른 값으로 채울 수 있습니다

```python
df['column'].fillna(something, inplace)
```

- Column : 결측치를 채울 열
- something : 조건
  - 결측치를 어떻게 채울지 결정할 수 있는 매개변수입니다.
  - 모든 결측치를 특정한 값으로 채워넣으려면 int 값이나 변수를 넣으면 됩니다.
  - 특정한 값으로 채워넣는 방법은 다음과 같습니다.
    - Method = fill : 바로 앞의 인덱스의 값으로 채우기
    - Method = bfill : 바로 뒤의 인덱스의 값으로 채우기
  - fillna() 메서드 대신 interpoltae() 메서드를 이용하여 선형보간법으로 결측치를 채워 넣을 수 있습니다.

```python
# Example
air_text['Ozone'].interpolate(method = 'linear', inplace = True)
```

### 가변수 (Dummy Variable) 만들기

- 가변수란?
  - 범주형 데이터를 독립된 열로 변환한 것
  - 가변수를 만드는 과정 => 'One-Hot-Encoding'
  - Get_dummies() 함수를 사용해서 가변수를 만들 수 있습니다.

```python
import pandas as pd
pd.get_dummies(df, columns, drop_first)
```

- df : 가변수를 만들 데이터프레임
- columns : 가변수를 만들 열
  - List 를 이용하여 한 번에 처리할 수 있습니다.
  - 지정하지 않으면 object 값을 가지는 모든 열이 대상이 됩니다.
  - 기존 열은 자동으로 제거되며, 열 이름은 prefix 로 지정됩니다.
- Drop_first : 첫 열 버리기
  - True 입력시, 첫번째 열을 버릴 수 있습니다.

------

## 데이터프레임 합치기

### Concat(합치기)

- 데이터를 물리적으로 합칠 수 있습니다.

```python
pd.concat([df1, df2], join, axis)
```

- Df : 합칠 데이터프레임
- join : 합칠 옵션 (기본값: join = 'outer')
  - 인덱스 혹은 열이 다른 경우 빈 값이 생기는 열 혹은 행을 결측치로 채우는 옵션이 'outer', 완전하게 제거하는 옵션이 'inner' 입니다.
- axis : 합칠 방향 (기본값 : 0)
  - 0 이면 세로
  - 1 이면 가로

### Join(병합)

- merge() 함수를 이용하여 두 데이터프레임을 지정한 키 값 기준으로 병합할 수 있습니다.
- 가로로만 붙일 수 있습니다.

```python
import pandas as pd
pd.merge(df1, df2, on, how)
```

- df : 합칠 데이터프레임
  - Concat 와 달리 list 로 묶여있지 않습니다.
  - How 값에 따라 합치는 순서에 영향이 있습니다.
- On : 합칠 기준이 될 키 값(열)
  - 같은 이름의 열이 있으면 지정하지 않아도 자동으로 조인됩니다.
  - 명시적으로 지정하는 권고됩니다.
- How : 병합 기준 (기본값 : how = 'inner')
  - left
    - 왼쪽 데이터(df1)을 기준으로 병합합니다.
    - 왼쪽에 있는 열은 결측치로 채우고 없는 열은 삭제합니다.
  - right
    - 오른쪽 데이터(df2)을 기준으로 병합합니다.
    - 오른쪽에 있는 열은 결측치로 채우고 없는 열은 삭제합니다.
  - Outer
    - 빈 값이 생기는 모든 데이터를 결측치로 채웁니다.
    - 합집합과 유사합니다.
  - Inner 
    - 빈 값이 생기는 모든 데이터의 행과 열을 삭제합니다.
    - 교집합과 유사합니다.
