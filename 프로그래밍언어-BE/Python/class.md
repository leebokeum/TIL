### class
~~~ python
class Person:
    #self는 자기자신 this같은 역할
    def greeting(self):
        print("안녕하세요")
    def sing(Self):
        self.greeting()
        print("랄라라)

a = Person()
a.greeting()
a.sing()
~~~


### init 초기화(생성자 같은 역할)
~~~ python
class Person:
    def __init__(self, name, age, live):
        self.name =name
        self.age = age
        self.live = live

    #self는 자기자신 this같은 역할
    def greeting(self):
        print("안녕하세요") 

a = Person("이복음", 20, "서울")
a.name
~~~

### 필드 정의
~~~ python
class Person:
    sex = ""
    items = []
    def __init__(self, name, age, live):
        self.name =name
        self.age = age
        self.live = live

    #self는 자기자신 this같은 역할
    def addItem(self, item):
        self.items.append(item) 
    
    def getItems(self):
        print(self.items)


a = Person("이복음", 20, "서울")
a.additem("랩탑")
a.getItems()
~~~

### private 속성 __
~~~ python
class Person:
    __sex = ""
    __items = []
    def __init__(self, name, age, live):
        self.name =name
        self.age = age
        self.live = live

    #self는 자기자신 this같은 역할
    def addItem(self, item):
        self.__items.append(item) 
    
    def getItems(self):
        print(self.__items)


a = Person("이복음", 20, "서울")
a.additem("랩탑")
a.getItems()
~~~

### 정적 매소드(static method)
~~~ python
class Calc:
    # 정적메소드에서는 self가 필요없다.
    @staticmethod  
    def add(a, b):
        return a + b
~~~
- 정적 메소드가 들어 있는 클래스는 정적 클래스가 되고 이는 정적 클래스는 생성없이 바로 사용 가능하다.


### 상속
~~~ python
class Person: 
    def __init__(self, name, age, live):
        self.name =name
        self.age = age
        self.live = live

    def greeting(self):
        print("안녕하세요") 


## 상속
class Student(Person):
    #pass는 부모 클래스와 똑같은 것을 의미
    pass

p1 = Student("이복음", 20, "서울")
p1.greeting()

class Teacher(Person):

    def __init__(self, name, age, live, teacher_id):
        self.name =name
        self.age = age
        self.live = live
        self.teacher_id = teacher_id

    #overiding
    def greeting(self):
        super().greeting()
        print("선생님입니다")

    def study(self): 
        print("공부중")    
    
~~~


## 다중 상속
~~~ python
class University:
    Uni_name = ""
    Uni_address = ""

#다중 상속
class CollegeStudent(Teacher, University):
    pass
~~~