# Comma separte value(csv)

- csv, 필드를 쉽표로 구분한 텍스트 파일
- 엑셀 양식의 데이터를 프로그램에 상관없이 쓰기 위한 데이터 형식
- 탭(TSV), 빈칸(SSV) 등으로 구분해서 만들기도 함

- 통칭하며 character separated values(CSV)
- 엑셀에서는 '다른 이름 저장' 기능으로 사용 가능



__엑셀로 CSV 파일 만들기__

1) 파일 다운로드
2) 파일 열기
3) 파일 -> 다른 이름 저장 -> CSV 선택
4) 엑셀 종료 후 notepad로 파일 열어보기



__파이썬으로 CSV 파일 읽기/쓰기__

- 일반적 textfile을 처리하듯 파일을 읽어온 후, 한줄 한 줄씩 데이터를 처리함

```python
line_counter = 0
data_handler = [] # 데이터의 헤드
customer_list = [] # customer 개별 리스트

with open ('customer.csv') as f:
    while True:
        data = f.readline()
        if not data: break
        if line_counter == 0:
            data_handler = data.split(',')
        else:
            customer_list.append(data.split(','))
        line_counter += 1
```



__csv 객체로 csv 처리__

- text 파일 형태로 데이터 처리시 전처리 과정이 필요
- 파이썬에서는 간단히 csv 파일을 처리하기 위해 csv 객체를 제공함

```python
import csv
reader = csv.reader(f,
                   delimiter = ','
                   quotechar="'",
                   quoting=csv.QOUTE_ALL)
```



# Web

- 인터넷 = Web
- 데이터 송수신을 위한 HTTP 프로토콜 사용
- 데이터를 표시하기 위해 HTML 사용



__web은 어떻게 동작하는가?__

1. 요청: 웹주소, form, header 등
2. 처리: Database 처리 등 요청 대응
3. 응답: HTML, XML 등으로 결과 반환



# HTML(Hyper Text Markup Language)

- 웹상의 정보를 구조적으로 표현하기 위한 언어

- 제목, 단락, 링크 등 요소 표시를 위해 Tag 사용

- 모든 요소들은 꺾쇠 괄호 안에 둘러 쌓여 있음

  ex) <title> Hello, World</title>

- 모든 HTML은 트리 모양의 포함 관계를 가짐

- HTML 소스파일을 컴퓨터 브라우저가 해석



__왜 웹을 알아야 하는가?__

- 정보의 보고, 많은 데이터들이 웹을 통해 공유됨
- HTML도 일종의 프로그램, 페이지 생성 규칙이 있음: 규칙을 분석하여 데이터의 추출이 가능
- 추출된 데이터를 바탕으로 하여 다양한 분석이 가능



__정규식(regular expression)__

- 복잡한 문자열 패턴을 정의하는 문자 표현 공식
- 특정한 규칙을 가진 문자열의 집합을 추출
- HTML 역시 tag를 사용한 일정한 형식이 존재하여 정규식으로 추출이 용이함
- 문법은 매우 방대, 스스로 찾아서 하는 공부 필요

__정규식 연습장 활용하기: regexr.com__

 

__정규식 기본 문법 - 메타문자__

- 정규식 표현을 위해 다른 용도로 사용되는 문자
- {m, n}: 반복 횟수를 지정
- ?: 반복 횟수가 1회
- |: or, ^: not



__정규식 in 파이썬__

- re모듈을 import하여 사용
- 함수: search - 한개만 찾기, findall - 전체 찾기
- 추출된 패턴은 tuple로 반환 됨

```python
import re
import urllib.request

url = 'hhtps://bit.ly/3rxQFS4'
html = urllib.request.urlopen(url)
html_contents = str(html.read())
id_results = re.findall(r'([A-Za-z0-9]+\*\*\*)', html_contents)

for result in id_results:
    print(result)
```



# XML(extensive markup language)

- 데이터의 구조와 의미를 설명하는 Tag를 사용하여 표시하는 언어
- Tag와 Tag 사이에 값이 표시되고 구조적인 정보를 표현할 수 있음
- HTML과 문법이 비슷, 대표적인 데이터 저장 방식



__XML이란__

- 정보 구조에 대한 정보인 스키마와 DTD 등으로 정보에 대한 정보가 표현되며, 용도에 따라 다양한 형태로 변경가능
- XML은 컴퓨터(PC와 스마트폰)간에 정보를 주고 받기 매우 유용한 저장 방식으로 쓰이고 있음



__Beautifulsoup__

- html, xml등 markup 언어 scraping을 위한 대표적인 도구
- lxml과 html5lib 과 같은 parser를 사용함
- 속도는 상대적으로 느리나 간편히 사용할 수 있음

```python
# 모듈 호출
from bs4 import BeautifulSoup

# 객체 생성
soup = BeautifulSoup(books_xml, 'lxml')
# 태그 찾는 함수 find_all 생성
for book_info in soup.find_all('author'):
    print(book_info.get_text())
```



# JavaScript Object Notation

- 원래 웹 언어인 java Script의 데이터 객체 표현 방식
- 간결성으로 기계/인간이 모두 이해하기 편한
- 데이터 용량이 적고, code로 전환이 편함
- xml 대체제로 많이 활용 됨



__Json overview__

- python의 dict type과 유사
- key:value 쌍으로 전환 가능



__Json in python__

- 데이터 저장 및 읽기는 dict type과 상호호환 가능
- 웹에서 제공하는 API는 대부분 정보 교환시 Json 활용



```python
import json

# 읽기
with open('json_example.json', 'r', encoding='utf8') as f:
    contents = f.read()
    json_data = json.loads(contents)

# 쓰기
dict_data = {'name':'Zara', 'Age':7, 'Class':'First'}
    
with open('data.json', 'w') as f:
    json.dump(dict_data, f)
```

