# pandas

- 구조화 된 데이터 처리를 지원하는 라이브러리
- python계의 엑셀

- panel data - > pandas
- 고성능 array 계산 라이브러리인 numpy와 통합하여 강력한 '스프레드시트' 처리 기능을 제공
- 인덱싱, 연산용 함수, 전처리 함수 등을 제공함
- 데이터 처리 및 통계 분석을 위해 사용



__데이터 로딩__

- pd.read_csv: csv 읽어옴
- head(): 처음 다섯 행 출력
- columns: 컬럼 이름 지정



# series

- DataFrame: 데이터 테이블 전체를 포함하는 object

- 데이터 프레임중 하나의 column에 해당하는 데이터의 모음 object

- 데이터, 인덱스로 구성됨

```python
import pandas as pd
list_data = [1, 2, 3, 4, 5]
list_name = ['a', 'b', 'c', 'd', 'e']
sample_obj = pd.Series(data=list_data, index=list_name)

sample_obj['a'] # 인덱스로 접근하기
sample_obj['a'] = 3.2 # 인덱스로 할당하기
sample_obj.astype(int) # 타입 변경
sample_obj.values # 값 리스트만
sample_obj.index # 인덱스 리스트만
sample_obj.name # 컬럼 이름 지정
```

- 인덱스 값을 기준으로 series 생성, 인덱스가 데이터보다 많으면 NaN 추가



# DataFrame

- 데이터 테이블 전체를 포함하는 object
- series를 모아서 만든 데이터 테이블 = 기본 2차원

```python
raw_data = {'first_name':['Jason', 'Molly', 'Tina', 'Jake', 'Amy'],
           'last_name':['Miller', 'Jaconbson', 'Ali', 'Milner', 'Cooze'],
           'age':[42, 52, 36, 24, 73],
           'city':['San Francisco', 'Baltimore', 'Douglas', 'Boston']}

df = pd.DataFrame(raw_data, colums = ['first_name', 'last_name', 'age', 'city'])

# column 선택 방법 - Serise 데이터
df.first_name
df['first_name']
```



__DataFrame indexing__

- loc[index, column]: 인덱스 이름으로 접근
- iloc: 숫자로 변형



__DataFrame handling__

```python
df.debt = df.age > 40 #column에 새로운 값 할당

values = Serise(data=['M', 'F', 'F'], index=[0, 1, 3])
df['sex'] = values

df.T # transpose
df.values # array 타입으로 값 출력
df.to_csv() # csv형태로 출력

del df['debt'] # 컬럼 삭제
df.drop('debt', axis=1)
```



__selection with column names__

- 컬럼 하나: df['column']
- 컬럼 하나 이상: df[[column_1, column_2, column_3]]



__selection with index number__

- df[:1]
- 한 개 이상 인덱스: df[0, 1, 2]
- 불리언: df[column < 500]



__basic, loc, iloc selection__

- basic: df[['column_1', 'column_2']]
- loc: df.loc[1, 1]
- iloc: df.iloc[1, 1]



__index 재설정__

- df.index = list: 인덱스 할당
- df.reset_index(inplace=True): 인덱스 리셋, inplace - 원본 데이터를 변경함



__data drop__

- df.drop(index, inplace=True): 해당 인덱스 삭제



# dataframe operation

__serise operation__

- index를 기준으로 연산 수행, 겹치는 index가 없을 경우 NaN 반환
- fill_value: NaN값 0으로 바꿔서 계산



__series + dataframe__

- axis를 기준으로 row broadcasting 실행
- df.add(s2, __axis=0__)



# lambda, map, apply

- pandas의 series type에도 map 함수 사용 가능
- function 대신 dict, sequence 자료등으로 대체 가능

```python
s1 = Series(np.arange(10))
s1.map(lambda x:x**2).head()

z = {1:'A', 2:'B', 3:'C'}
s1.map(z).head()
#dict type으로 데이터 교체

s2 = Series(np.arange(10, 20))
s1.map(s2).head(5)
#같은 위치의 데이터를 s2로 전환
```



__apply for dataframe__

- map과 달리 series 전체에 해당 함수를 적용
- 입력 값이 series 데이터로 입력받아 handling 가능

- 내장 연산 함수를 사용할 때도 똑같은 효과를 거둘 수 있음
- mean, std, sum 등



__applymap for dataframe__

- series 단위가 아닌 element 단위로 함수를 적용함
- series 단위에 apply 적용시킬 때와 같은 효과



