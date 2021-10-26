# module and project

- 파이썬은 대부분의 라이브러리가 이미 다른 사용자에 의해서 구현되어 있음

 

# 그런데 어떻게 쓰이나요?

- 남이 만든 프로그램 쓰는 법 객체 > 모듈

 

# 모듈과 패키지

- 모듈은 하나의 패키지 안에 들어가 있음

- 모듈: 어떤 대상의 부분 혹은 조각

- 모듈 > 패키지 > 프로젝트(패키지 공개)

 

__모듈__

- 프로그램에서 사용하는 작은 프로그램 조각들

- 모듈을 모아서 하나의 큰 프로그램을 개발함

- 프로그램을 모듈화 시키면 다른 프로그램이 사용하기 쉬움 (ex. 카카오톡 게임을 위한 카카오톡 접속 모듈)

 

 

# 모듈 in python

- Built in module

```python
import random
random.randint(1, 1000)
```

 Built-in module인 random을 사용, 난수를 쉽게 생성할 수 있음

 

# 패키지

- 모듈을 모아놓은 단위, 하나의 프로그램

 

# 직접 구현을 해봐야 알 수 있다!

 

- 모듈 만들기

1. 파이썬의 module == py. 파일을 의미

2. 같은 폴더에 module에 해당하는 .py파일과 사용하는 .py파일을 저장한 후

3. Import문을 사용해서 module을 호출

```python
# fah_converter.py
def convert_c_to_f(celsius_value):
    return celsius_value * 9.0 / 5 + 32

# module_ex.py
Import fah_converter

print(‘Enter a celsius value: ‘)
celsius = float(input())
fahrenheit = fah_converter.convert_c_to_f(celsius)
print(‘That’s’, fahrenheit, ‘degrees Fahrenheit’)
```



- Name space

  - 모듈을 호출할 때 범위 정하는 방법

  - 모듈 안에는 함수와 클래스 등이 존재 가능

  - 필요한 내용만 골라서 호출 할 수 있음

  - From과 import 키워드를 사용함

    

> __Name space example__
>
> - Alias 설정하기 – 모듈명을 별칭으로 써서
>
> ```python
> import fah_converter as fah 
> ```
> - 모듈에서 특정 함수 또는 클래스만 호출하기
>
> ```python
> from fah_converter improt convert_c_to_f
> ```
> - 모듈에서 모든 함수 또는 클래스를 호출하기
>
> ```python
> from fah_converter import *
> ```



-	Built-in module
  - 파이썬이 기본적으로 제공하는 모듈
  - 수많은 파이썬 모듈들은 어떻게 쓸 것인가
    - 구글에 물어본다
    - Import후 help 사용
    - 파이썬 공식 문서를 읽어본다



# 패키지

- 하나의 대형 프로젝트를 만드는 코드의 묶음

-	다양한 모듈들의 합, 폴더로 연결됨
-	\_\_init\_\_, \_\_main\_\_등 키워드 파일명이 사용됨
-	다양한 오픈 소스들이 모두 패키지로 관리됨



# 패키지 만들기
1)	기능들을 세부적으로 나눠 폴더로 만듦
2)	각 폴더별로 필요한 모듈을 구현함
3)	1차 test python shell (폴더로 구성되어도 모듈처럼 from과 import로 호출가능)
4)	폴더별로 \_\_init\_\_.py 구성하기
- 현재 폴더가 패키지임을 알리는 초기화 스크립트
- 없을 경우 패키지로 간주하지 않음(3.3+ 부터는 x)
- 하위 폴더와 py파일(모듈)을 모두 포함함
- mport와 \_\_all\_\_ keyword 사용(ex. \_\_all\_\_ = [‘image’, ‘sound’, ‘stage’])
5)	\_\_main\_\_.py 만들기



> __패키지 내에서 다른 폴더의 모듈을 부를 때 상대 참조로 호출하는 방법__
>
> ```python
> from game.graphic.render import render_test # 절대 참조
> from .render import render_test # .현재 디렉토리 기준
> from ..sound.echo import echo_test # ..부모 디렉토리 기준                   
> ```



# 오픈 소스 라이브러리 사용하기
- 두개의 다른 패키지를 설치할 경우엔 패키지끼리 서로 충돌이 날 경우가 있다

- __가상환경 설정하기!__

  

# 가상환경 설정하기(virtual environment)
-	프로젝트 진행시 필요한 패키지만 설치하는 환경
-	다양한 패키지 관리 도구를 사용함
-	대표적인 도구 virtualenv와 conda가 있음
-	Virtualenv + pip: 가장 대표적인 가상환경 관리 도구
-	Conda: 상용 가상환경도구, miniconda 기본 도구, windows에서 장점



# conda 가상환경

-	conda create -n my_project python=3.9
-	conda activate my_project: 가상환경 진입
-	conda deactivate: 가상환경 나오기
-	conda install matplotlib: 가상환경에서 패키지 설치