# 파이썬을 개발하는 방법

만들어 놓은 코드를 재사용하고 싶다!
어떻게 코드를 구조화해야 다른 사람들이 내 코드를 가져가서 자기 용도에 맞게 쓸 수 있도록 할 수 있을까? 

__"객체"__





# 클래스와 객체 - 객체 지향 언어의 이해

C#, JAVA가 객체 지향 언어의 기본이었고 요즘엔 다른 언어들도 객체지향언어 컨셉을 차용해서 만들어진다.
다른 프로그래밍 언어를 이해하기 위해서도 객체지향언어를 알아야한다.

수강신청 프로그램을 작성한다 어떻게해야할까?

- 1번째 방법: 수강신청이 시작부터 끝까자 순서대로 작성

- 2번째 방법: 수강신청 관련 주체들(교수, 학생, 관리자)의 행동(수강신청, 과목 입력)과 데이터(수강과목, 강의 과목)들을 중심으로 프로그램 작성 후 연결

__2번째 방법 = 객체 지향 프로그램__





# 객체지향 프로그래밍 개요

- Object-Oriented Programming(OOP)
- 객체: 실생활에서 일종의 물건, 속성(attribute)과 행동(action)을 가짐
- OOP는 객체 개념을 프로그램으로 표현, 속성은 변수 행동은 함수로 표현됨
- 파이썬 역시 객체 지향 프로그램 언어

- OOP는 설계도에 해당하는 클래스(class)와 실제 구현체인 인스턴스(instance)로 나눔





# "직접 구현을 해봐야 알 수 있다!"

__1. 선수 정보를 class로 구현하기__

```python
class SoccerPlayer(object):
```
예약어 + class 이름 (상속받는 객체명):



> __변수와 class명 함수명은 짓는 방식이 존재__
>
>    - snake_case: 띄어쓰기 부분에 언더바 추가, 파이썬 함수, 변수명에 사용
>
>    - CamelCase: 띄어쓰기 부분에 대문자, 파이썬 class명에 사용
>
>         

__2. Attribute 추가하기__

```python
    def __init__(self, name, position, back_number):
        self.name = name
        self.position = position
        self.back_number = back_number
```
\__init__은 객체 초기화 예약함수
self: 인스턴스 자신



> __파이썬에서 \__의미__
>
>     - __ 는 특수한 예약 함수나 변수 그리고 함수명 변경(맨글링)으로 사용 ex) \__main\__, \__add\__, \__str\___, __eq\__
>
>
> - method 구현하기

```python
class SoccerPlayer(object):
    def change_back_number(self, new_number):
        print("선수의 등번호를 변경합니다 : From %d to %d" % (self.back_number, new_number))
        self.back_number = new_number
```
method 추가는 기존 함수와 같으나 반드시 self를 추가해야만 class 함수로 인정됨

__3. object 사용하기__

```python
jihyun = SoccerPlayer('jihyun', 'MF', 10)
```
객체명 = class명(\__init\__ 함수 interface, 초기값)



__예제 코드__

```python
class SoccerPlayer(object):
    def __init__(self, name, position, back_number):
        self.name = name
        self.position = position
        self.back_number = back_number
    
    def change_back_number(self, new_number):
        print("선수의 등번호를 변경합니다 : From %d to %d" % (self.back_number, new_number))
        self.back_number = new_number

    def __str__(self):
        return "Hello, My name is %s. My back number is %d" %(self.naem, self.back_number)
```



# OOP implementation example



## 구현 가능한 OOP 만들기 - 노트북

- 노트를 정리하는 프로그램
- 사용자느 노트에 뭔가 적을 수 있다
- 노트에는 컨텐츠가 있고 내용을 제거 할 수 있다
- 두개의 노트북을 합쳐 하나로 만들 수 있다
- 노트는 노트북에 삽입된다
- 노트북에 노트가 삽입 될 때 페이지르 ㄹ생서앟며 최고 300페이지 까지 저장 가능하다
- 300페이지가 넘으면 더 이상 노트를 삽입하지 못한다.



```python
class Note():
    def __init__(self, content):
        self.content = content
    
    def write_content(self, content):
        self.content = content
        
    def remove_all():
        self.content = ''
    
    def __add__(self, other):
        return self.content + other.content
    
    def __str__(self):
        return self.content
    
class Notebook():
    def __init__(self, title):
        self.title = title
        self.pages = {}
        self.n_pages = 0
        
    def add_note(self, note, page=0):
        if n_pages < 300:
            if page == 0:
                self.pages[n_pages] = note
                n_pages += 1
            else:
                self.pages[page] = note
                n_pages += 1
        else:
            print('page가 모두 채워졌습니다.')
    
    def remove_note(self, page_number):
        if page_number in pages.keys():
            return self.pages.pop(page_number)
        else:
            print('해당 페이지는 존재하지 않습니다.')
    
    def get_n_pages(self):
        return len(self.pages.keys())
```



# OOP characteristics



- 객체지향 언어의 특징: 실제 세상을 모델링
- 필요한 것들: __inheritance, polymorphism, visibility__



## inheritance

- 부모 클래스로 부터 속성과 method를 물려받은 자식 클래스를 생성하는 것



```python
class Person(object):
    def __init__(self, name, age, gender):
        self.name = name
        self.age - age
        self.gender = gender
        
class Employee(person):
    def __init__(self, name, age, gender, salary, hire_date):
        super().__init__(name, age, gender)
        self.salary = salary
        self.hire_date = hire_date
```



## 다형성

- 같은 이름의 메소드의 내부 로직을 다르게 작성
- Dynamic Typing 특성으로 인해 파이썬에서는 같은 부모 클래스의 상속에서 주로 발생함

```python
class Animal():
    def __init__(self, name):
        self.name = name
        
    def talk(self):
        raise Error
        
class Cat(Animal):
    def talk(self):
        return '야옹'

class Dog(Animal):
    def talk(self):
        return '멍멍'
```



## 가시성

- 객체의 정보를 볼 수 있는 레벨을 조절하는 것
- 누구나 객체 안에 모든 변수를 볼 필요가 없음
  - 객체를 사용하는 사용자가 임의로 정보 수정
  - 불필요한 변수 숨김



> __Encapsulation__
>
> - 캡슐화 또는 정보 은닉(information hiding)
> - class를 설계할 때, 클래스 간 간섭/정보공유의 최소화
> - 캡슐을 던지듯, 인터페이스만 알아서 써야함



```python
class Inventory():
    def __init__(self):
        self.__items = []
        # 언더바 2개로 private 변수 선언
        # 다른 객체에서 접근 불가
    
    @property # decorater로 접근 허용
    def items(self):
        return self.__items
```



# Decorate

__이해하기 위한 개념들__

- first-class object
  - 일등함수 또는 일급 객체
  - 변수나 데이터 구조에 할당이 가능한 객체
  - 파라미터로 전달 + 리턴 값으로 사용
  - 파이썬의 함수는 '일급함수'

- inner function

  - 함수 내에 또 다른 함수가 존재

  - ```python
    def print_msg(msg):
        def printer():
            print(msg)
        printer
    ```

  - __closure__: inner function을 return값으로 반환

  - ```python
    def tag_func(tag, text):
        text = text
        tag = tag
        
        def inner_func():
            return '<{0}>{1}<{0}>'.format(tag, text)
        
        return inner_func
    ```

- decotater function

  -  클로져 함수를 간단하게!

  - ```python
    def star(func):
        def inner(*args, **kwargs):
            print('*' * 30)
            func(*args, **kwargs)
            print('*' * 30)
        return inner
    
    @star
    def printer(msg):
        print(msg)
    ```

