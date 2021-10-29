# Numerical Python - Numpy

__"어떻게 행렬과 매트릭스를 코드로 표현할 것인가?"__

```python
coefficient_matrix = [[2, 2, 1], [2, -1, 2], [1, -1, 2]]
constant_vector = [9, 6, 5]
```

- 다양한 matrix 계산을 어떻게 만들 것인가?
- 굉장히 큰 matrix에 대한 표현(메모리 효율 x)
- 처리 속도 문제 - python은 interpreter 언어



__numpy__

- numerical python
- 파이썬의 고성능 과학 계산용 패키지
- matrix와 vector와 같은 array 연산의 사실상의 표준



__numpy의 특징__

- 일반 list에 비해 빠르고, 메모리 효율적
- 반복문 없이 데이터 배열에 대한 처리를 지원함
- 선형대수와 관련된 다양한 기능을 제공함
- C, C++, 포트란 등의 언어와 통합 가능



# ndarray

```python
import numpy as np

test_array = np.array([1, 4, 5, 8], float)
print(test_array)
type(test_array[3])
```

- np.array 함수를 통해 배열을 생성함
- numpy는 하나의 데이터 type만 배열에 넣을 수 있음
- list와 가장 큰 차이점: 다이나믹 타이핑 x
- C의 array를 사용하여 배열을 생성함



__array creation__

- ndarray는 데이터가 차례대로 메모리에 할당
- python 리스트는 데이터가 메모리에 차례대로 들어가는 것이 아니라 데이터의 주소를 리스트에 넣음(주소로 부터 메모리로 들어가는 단계를 한번 더 거쳐야 함)
- shape: array의 dimension 구성을 반환
- dtype: array의 데이터 타입을 반환



__array.shape__

- array의 rank에 따라 불리는 이름이 있음
- 0: scalar, 1: vector, 2: matrix, 3: 3-tensor, n: n-tensor
- ndim - number of dimensions = rank
- size - data의 갯수



__array.dtype__

- single element가 가지는 data type
- 각 element가 차지하는 memory의 크기가 결정됨(ex. np.float32, np.int8 ...)



__array.nbytes__

- nbytes: array object의 메모리 크기를 반환함



# Handling shape



__reshape__

- reshape: array의 shape의 크기를 변경함, element의 갯수는 동일

```python
import numpy as np
np.array(test_matrix).reshape(2, 4)
np.array(test_matrix).reshape(-1, 2)
# -1: size를 기반으로 row 갯수 선정
```



__flatten__

- flatten: 다차원 array를 1차원 array로 변환

```python
np.array(test_matrix).flatten()
```



# indexing & slicing

- list와 달리 이차원 배열에서 [0, 0] 표기법을 제공함
- matrix일 경우 앞은 row 뒤는 column을 의미함

```python
a = np.array([[1, 2, 3], 
              [4, 5, 6]])

print(a[0][2])
print(a[0, 2])
a[0, 2] = 10 # 0, 2에 10 할당
```



- 리스트와 달리 행과 열을 나눠서 slicing이 가능함
- matrix의 부분 집합을 추출할 때 유용함

```python
a = np.array([[1, 2, 3, 4, 5],
             [6, 7, 8, 9, 10]])

a[:, 2:] # 전체 row의 2열 이상
a[1, 1:3] # 1 row의 1~2열
a[1:3] # 1~2 row 전체
```

- a[start : end : step]



__creation function__

- arange: array의 범위를 지정하여 값의 list를 생성하는 명령어
- zeros: 0으로 가득찬 array 생성
- ones: 1로 가득찬 array 생성
- empty: memory만 주어지고 비어있는 array 생성
- somthing_like: array의 shape 크기 만큼 1, 0, 또는 empty array를 반환



__identity__

- 단위 행렬을 생성함



__eye__

- 대각선의 값이 1인 행렬, k값의 시작 index의 변경이 가능



__diag__

- 대각 행렬의 값을 추출함, k값 지정 가능



__random sampling__

- 데이터의 분포에 따른 sampling으로 array 생성

```python
np.random.uniform(0, 1, 10).reshape(2, 5)
```



# operation functions

__sum__

- array의 element 간의 합



__axis__

- 모든 operation function을 실행할 때 기준이 되는 dimension 축
- (3, 4): axis = 0은 3, axis = 1은 4



__mean & std__

- array의 element들 간의 평균 또는 표준편차를 반환



__mathmatical functions__

- 그 외에도 다양한 수학 연산자를 제공함



__concatenate__

- array를 합치는 함수
- vstack: 세로로 붙이기
- hstakc: 가로로 붙이기
- concatenate: axis를 기준으로 붙임
- np.newaxis: 축을 추가해줌



__operations b/t array__

- numpy는 array간의 기본적인 사칙 연산을 지원함
- element-wise operations: array간 shape이 같을 때, 같은 위치에 있는 element끼리 연산



__Dot product__

- matrix의 기본연산, dot 함수 사용

```python
test_a.dot(test_b)
```



__transpose__

- transpose 함수 또는 T attribute 사용



__broadcasting__

- shape이 다른 배열 간 연산을 지원하는 기능

```python
test_matrix = np.array([[1, 2, 3],
                       [4, 5, 6]])
scalar = 3
print(test_matrix + scalar)
```

- scalar-vector 외에도 vector-matrix 간의 연산도 지원



__numpy performace__

- timeit: jupyter 환경에서 코드의 퍼포먼스를 측정하는 함수
- 일반적인 속도: for loop < list comprehension < numpy
- numpy는 C로 구현되어 있어 성능을 확보하는 대신 dynamic typing을 포기함
- concatenate 처럼 계산이 아닌 할당에서는 연산 속도의 이점이 없음



# comparison



__All & Any__

- array의 데이터 전부 또는 일부가 조건에 만족 여부 반환



__comparison operation__

- 배열의 크기가 동일할 때, element간 비교의 결과를 boolean type으로 반환(element-wise)
- logical_and, logical_not, logical_or



__np.where__

```python
np.where(a > 0, 3, 2) # where(condition, True, False)

a = np.arange(10)
np.where(a>5) # index 값 반환

a = np.array([1, np.NaN, np,Inf])
np.isnan(a)
np.isfinite(a)
```



__argmax & argmin__

- array내 최대값 또는 최소값의 index 반환
- axis 기반의 반환

```python
a = np.array([[1, 2, 4, 7],
             [9, 88, 6, 45],
             [9, 76, 3, 4]])

np.argmax(a, axis=1)
# array([3, 1, 1])
```

- argsort(): 오름차순으로 정렬한 index 반환



# boolean & fancy index

__boolean index__

- 특정 조건에 따른 값을 배열 형태로 추출
- comparison operation 함수들도 모두 사용 가능

```python
test_array = np.array([1, 4, 0, 2, 3, 8, 9, 7])

test_array[test_array > 3]
```



__fancy index__

- array를 index value로 사용해서 값 추출

```python
a = np.array([2, 4, 6, 8])
b = np.array([0, 0, 1, 3, 2, 1]) # 반드시 integer로 선언
a[b] # b 배열의 값을 index로 하여 a 값을 추출함
a.take(b) # bracket index와 같은 효과
```

- matrix도 사용 가능



# numpy data i/o



__loadtxt & savetxt__

- text type의 데이터를 읽고 저장하는 기능

```python
a = np.loadtxt('population,txt', delimiter='\t')

np.savetxt('int_data_2.csv', a_int_3, fmt='%.2e', delimiter=',')
```



__numpy object - npy__

```python
np.save('npy_test.npy', arr=a_int)

npy_array = np.load(file='npy_test.npy')
```

- 피클 형태로 저장