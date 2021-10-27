# 프로그램 사용할 때 일어나는 오류들

- 주소를 입력하지 않고 배송 요청

- 저장도 안했는데 컴퓨터 전원이 나감

- 게임 아이템 샀는데 게임에서 튕김

  __exception__

  1) 예상이 가능한 예외
  2) 예상이 불가능한 예외



### 예상 가능한 예외

- 발생 여부를 사전에 인지할 수 있는 예외
- 사용자의 잘못된 입력, 파일 호출 시 파일 없음
- 개발자가 반드시 명시적으로 정의 해야 함

### 예상이 불가능한 예외

- 인터프리터 과정에서 발생하는 예외, 개발자 실수
- 리스트의 범위를 넘어가는 값 호출, 정수 0으로 나눔
- 수행 불가시 인터프리터가 자동 호출



# 예외 처리

- 예외가 발생할 경우 후속 조치 등 대처 필요
  1) 없는 파일 호출 -> 파일 없음을 알림
  2) 게임 이상 종료 -> 게임 정보 저장
- 프로그램 = 제품, 모든 잘못된 상황에 대처가 필요

__"Exception Handling"__



# Exception handling

__try ~except 문법__

```python
try:
    # 예외 발생 가능 코드
except <Exception Type>:
    # 예외 발생 시 대응하는 코드
```



__예시. 0으로 숫자를 나눌 때 예외 처리__

```python
for i in range(10):
    try:
        print(10/i)
    except ZeroDivisionError:
        print('Not divided by 0')
```

__built-in Exception: 기본적으로 제공하는 예외__

- IndexError: 리스트 인덱스 범위를 넘어갈 때
- NameError: 존재하지 않은 변수 호출
- ZeroDivisionError: 0으로 숫자를 나눌 때
- ValueError: 변환할 수 없는 문자/숫자를 변환할 때
- FileNotFoundError: 존재하지 않는 파일 호출



__try~except~else__

```python
try:
    # 예외 발생 가능 코드
except <Exception Type>:
    # 예외 발생 시 대응하는 코드
else:
    # 예외가 발생하지 않았을 경우
```



__try~except~finally__

```python
try:
    # 예외 발생 가능 코드
except <Exception Type>:
    # 예외 발생 시 대응하는 코드
finally:
    # 예외가 발생했을 경우, 안했을 경우 모두 실행
```



__raise 구문__

- 필요에 따라 강제로 Exception을 발생

```python
while True:
    value = input('변환할 정수 값을 입력해주세요')
    for digit in value:
        if digit not in '0123456789':
            raise ValueError('숫자값을 입력하지 않으셨습니다')
    print('정수 값으로 변환한 숫자')
```



__assert 구문__

- 특정 조건에 만족하지 않을 경우 예외 발생

```python
def get_binary_number(decimal_number):
    assert isinstance(dicimal_number, int)
    return bin(decimal_number)
```



# File handling

- __File System__: OS에서 파일을 저장하는 트리구조 저장 체계
- __File from wiki__: 컴퓨터 등의 기기에서 의미 있는 정보를 담는 논리적인 단위. 모든 프로그램은 파일로 구성되어 있고 파일을 사용한다.



__파일의 종류__

- 기본적인 파일 종류로 text 파일과 binary 파일로 나눔
- 컴퓨터는 text 파일을 처리하기 위해 binary 파일로 변환시킴
- 모든 text 파일도 실제는 binary 파일
- ASCII/Unicode 문자열 집합으로 저장되어 사람이 읽을 수 있음

|                         Binary 파일                          |                          Text 파일                           |
| :----------------------------------------------------------: | :----------------------------------------------------------: |
| - 컴퓨터만 이해할 수 있는 형태인 이진법 형식으로 저장된 파일, 일반적으로 메모장으로 열면 내용이 깨져보임(엑셀파일, 워드파일 등등) | - 인간도 이해할 수 있는 형태인 문자열 형식으로 저장된 파일, 메모장으로 열면 내용 확인 가능(메모장에 저장된 파일,  HTML  파일, 파이썬 코드 파일 등) |



__Python File I/O__

- 파이썬은 파일 처리를 위해 open 키워드를 사용함



__파이썬의 File read__

- read(): text 파일안에 있는 내용을 문자열로 반환

```python
f = open('dream.txt', 'r')
contents = f.read()
print(contents)
f.close()
```

- with 구문과 함께 사용하기

```python
with open('dream.txt', 'r') as f:
    # 파일 전체를 리스트로 변환
    content_list = f.readlines()
```

- 실행 시마다 한 줄 씩 읽어 오기 (한 줄 씩 읽으면서 그때 그때 메모리에 올리기)

```python
with open('dream.txt', 'r') as f:
    i = 0
    while True:
        line = f.readline()
        if not line:
            break
        print(str(i) + '===' + line.replace('\n', '')) # 한 줄 씩 값 출력
        i += 1
```



__파이썬의 File Write__

- mode는 'w', encoding='utf8'

```python
f = open('count.txt', 'w', encoding='utf8')
for i in range(1, 11):
    data = '%d번째 줄입니다\n' % i
    f.write(data)
f.close()
```



- mode 'a'는 추가 모드

```python
with open('count.txt', 'a', encoding='utf8') as f:
    for i in range(1, 11):
        data = '%d번째 줄입니다.\n' % i
        f.write(data)
```



__파이썬의 directory 다루기__

```python
import os
os.mkdir('log') # log 폴더 만들기
os.path.exists('log') # 폴더가 있는지 확인

import shutil
source = 'dream.txt'
dest = os.path.join('abc', 'sc.txt')
# os마다 폴더 seperator가 다르기 때문에 join을 사용한다.
shutil.copy(source, dest) # 파일 복사
```

- 최근에는 pathlib 모듈을 사용하여 path를 객체로 다룸

```python
import pathlib

cwd = pathlib.path.cwd()
print(cwd.parent) # 부모 폴더
print(list(cwd.parents)) # 부모 폴더 리스트
print(list(cwd.glob('*')) # 폴더 내 모든 파일
```



__예제. Log 파일 생성하기__

```python
import os
if not os.path.isdir('log'):
    os.mkdir('log')
if not os.path.exists('log/count_log.txt'):
    f = open('log/count_log.txt', 'w', encoding='utf8')
    f.write('기록이 시작됩니다\n')
    f.close
    
with open('log/count_log.txt', 'a', encoding='utf8') as f:
    import random, datetime
    for i in range(1, 11):
        stamp = str(datetime.datetime.now())
        value = random.random() * 1000000
        log_line = stamp + '\t' + str(value) + '값이 생성되었습니다' + '\n'
        f.write(log_line)
    
```



__Pickle__

- 파이썬의 객체를 영속화(파일로 씀)하는 built-in 객체
- 데이터, object 등 실행중 정보를 저장 -> 불러와서 사용
- 저장해야하는 정보, 계산 결과(모델) 등 활용이 많음
- Binary 파일

```python
import pickle

f = open('list.pickle', 'wb')
test = [1, 2, 3, 4, 5]
pickle.dump(test, f) # 피클에 저장
f.close()

f = open('list.pickle', 'rb')
test_pickle = pickle.load(f) # 피클 열기
test_pickle
f.close()
```



# Logging handling



__logging__

- 프로그램이 실행되는 동안 일어나는 기록을 남기기
- 유저의 접근, 프로그램의 Exception, 특정 함수의 사용
- 어디에? - console 화면에 출력, 파일에 남기기, DB에 남기기 등등
- 기록된 로그를 분석하여 의미있는 결과를 도출 할 수 있음
- 실행시점에서 남겨야 하는 기록, 개발시점에서 남겨야 하는 기록



__print vs logging__

- 기록을 print로 남기는 것도 가능
- 그러나 console 창에만 남기는 기록은 분석시 사용 불가
- 때로는 레벨별(개발, 운영)로 기록을 남길 필요도 있음
- 모듈별로 별도의 logging을 남길 필요도 있음
- 이런 기능을 체계적으로 지원하는 모듈이 필요함



__logging level__

- 프로그램 진행 상황에 따라 다른 레벨의 로그를 출력함
- 개발시점, 운영시점 마다 다른 로그가 남을 수 있도록 지원함
- debug > info > warning > error > critical
- log 관리시 가장 기본이 되는 설정 정보

```python
import logging

logging.debug #개발시 처리 기록을 남겨야하는 로그 정보
logging.info # 처리가 진행되는 동안의 정보
logging.warning # 사용자가 잘못 입력한 정보다 원래 개발시 의도치 않는 정보가 들어왔을 때
logging.error # 잘못된 처리로 에러가 났으나, 프로그램은 동작할 수 있음
logging.critical # 잘못된 처리로 데이터 손실이나 더이상 프로그램이 동작할 수 없음을 알림
```

- 기본 레벨은 warning부터 사용자가 확인 가능
- logging.basicConfig()로 기본 레벨 변경 가능
- logging.FileHandler(): 파일에 로그 저장



__configparser__

- 프로그램의 실행 설정을 file에 저장함
- section, key, value 값의 형태로 설정된 설정 파일을 사용
- 설정파일을 dict type으로 호출 후 사용

```python
import configparser
config = configparser.ConfigParser()

config.read('example.cfg')
config.sections()

for key in config['SectionOne']:
    print(key)
    
config['SectionOne']['status']
```



__argparser__

- console 창에서 프로그램 실행시 setting 정보를 저장함
- 거의 모든 console 기반 python 프로그램 기본으로 제공
- 특수 모듈도 많이 존재하지만(TF), 일반적으로 argparse를 사용
- Command-Line option이라고 부름

```python
import argparse

parser = argparse.ArgumentParser(description='Sum two integers.')

parser.add_argument('-a', '--a_value', dest='A_value', help='A integers', type=int)
parser.add_argument('-b', '--b_value', dest='B_value', help='B integers', type=int)

args = parser.parse_args()
print(args)
print(args.a)
print(args.b)
print(args.a + args.b)
```



__Logging formater__

- 로그 결과값의 format을 지정해줄 수 있음

```python
formatter = logging.Formatter('%(asctime)s %(levelname)s %(process)d %(message)s/')
```



__Log config file__

```python
logging.config.fileConfig('logging.conf')
logger = logging.getLogger()
```



__