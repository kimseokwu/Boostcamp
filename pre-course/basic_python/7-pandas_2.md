# Groupby-1

- SQL groupby 명령어와 같음
- split -> apply -> combine 과정을 거쳐 연산함

```python
df.groupby('Team')['Points'].sum()
```

- 한 개 이상의 column을 묶을 수 있음

```python
df.groupby(['Team', 'Year'])['Points'].sum()
```



__hierarchical index__

- groupby 명령의 결과물도 dataframe
- 두개의 column으로 groupby를 할 경우, index가 두개 생성
- unstack(): 그룹으로 묶여진 데이터를 matrix 형태로 바꿔 줌
- swaplevel(): 인덱스 레벨을 바꿔 줌
- sort_index(level=0): 레벨을 기준으로 sort
- index level을 기준으로 기본 연산 수행 가능



# Groupby-2

- groupby에 의해 split 된 상태를 추출 가능함

```python
grouped = df.groupby('Team')

for name, group in grouped:
    print(name)
    print(group)
```

- tuple 형태로 그룹의 key, value 값이 추출 됨
- get_gorup(group_name): 특정 그룹의 정보를 가져올 수 있음
- 추출된 그룹 정보에는 세 가지 유형의 apply가 가능함
- Aggregation: 요약된 통계 정보를 추출해줌
- Transformation: 해당 정보를 변환해줌
- Filtration: 특정 정보를 제거하여 보여주는 필터링 기능



# pivot table & crosstab

__pivot table__

- index 축은 groupby와 동일함
- column에 추가로 labeling 값을 추가하여 
- value에 numeric type 값을 aggregation 하는 형태

```python
df_phone.pivot_table(value=['duration'],
                    index=[df_phone.month, df_phone.item],
                    columns=df_phone.network,
                    aggfunc='sum',
                    fill_value=0)

# groupby로 구현

df_phone.groupby(['month', 'item', 'network'])['duration'].sum().unstack()
```



__crosstab__

- 두 칼럼의 교차 빈도, 비율, 덧셈등을 구할 때 사용
- pivot table의 특수한 형태 
- user-item rating matrix등을 만들 때 사용 

```python
pd.crosstab(index=df_movie.critic,
           columns=df_movie.title,
           values=df_movie.rating,
           aggfunc='first',
           ).fillna(0)
```



# merge & concat



__merge__

- SQL에서 사용하는 merge와 같은 기능
- 두개의 데이터를 하나로 합침

```python
pd.merge(df_a, df_b, on='subject_id')
pd.merge(df_a, df_b, left_on='subject_id', right_on='subject_id') # 두 dataframe의 column 이름이 다를 때
```



__join method__

- inner join: 양쪽 테이블에 같은 subject_id가 있어야 함
- left/right join: 어느 한 쪽을 기준으로 join, 없는 것은 NaN 처리
- full(outer) join: 같은 것은 join하고 다른 것은 NaN



__index based join__

```python
pd.merge(df_a, df_b, right_index=True, left_index=True)
```



__concat__

- 같은 형태의 데이터를 붙이는 연산작업

```python
pd.concat([df_a, df_b], axis=1)
```

- 예제) 날짜 별로 다른 파일에 저장이 되어 있을 때

```python
import os
import pandas as pd

files = [file_name for file_name in os.listdir('./data') if file_name.endswith('xlsx')]

df_list = [pd.read_excel(os.path.join('data', df_filename) for df_filename in files)]
status = df_list[0]
sales = pd.concat(df_list[1:])
```



# persistence



__Database connection__

- data loading시 db connection 기능 제공함

```python
import sqlite3

conn = sqlite3.connect('./data/flights.db')
cur = conn.cursor()
cur.execute('select * from airlines limit 5;')
result = cur.fetchall()
result

df_airlines = pd.read_sql_query('select * from airlines;', conn)
df_airlines
```



__XLS persistence__

- dataframe의 엑셀 추출 코드
- xls 엔진으로 openpyxls 또는 XlsxWrite 사용

```python
writer = pd.ExcelWriter('./data/df_routes.xlsx', engine='xlsxwriter')
df_routes.to_excel(writer, sheet_name='Sheet1')
```



