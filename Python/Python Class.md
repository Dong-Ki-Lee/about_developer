# Python Class

여기서는 Python 의 Class에 대해서 다뤄보고자 한다.

C++, Java 등의 언어와 다른점을 집중적으로 볼 것이다.

## Method 의 self

python class 에서는 method 를 정의할 때 항상 self 라는 인자를 써준다.

```python
def hello(self):
    return 'hello'

def setdata(self, first, second):
    self.first = first
    self.second = second
```

위와 같이 첫번째 인자로 self 라는 인자가 들어가게 된다.

이 self 는 그 method를 호출한 객체가 들어가게 되는데, 예를 들어 a.hello() 라고 호출하게 된다면 a라는 객체가 self 라는 매개변수로 자동으로 전달된다. 다른 객체지만 같은 class 의 method를 사용하므로, 객체를 구별하기 위한 것이라고 볼 수 있다.

## Class variable VS Instance Variable

Python 에서는 클래스 변수와 객체 변수가 있는데, 먼저 예를 든 뒤에 설명하도록 한다.

```python
class Account:
    num_accounts = 0
    def __init__(self, name):
        self.name = name
        Account.num_accounts += 1
    def __del__(self):
        Account.num_accounts -= 1
```

> init과 del의 의미는 아래에서 다룬다.

여기서 num_accounts 가 class variable이 되고, name 이 instance variable이 된다.

차이점이라고 한다면, 그 이름의 뜻 그대로 class variable의 경우 그 클래스가 가지는 값이기 때문에 Account라는 여러 객체가 생겨도 num_accounts 라는 변수는 모든 객체에서 공통으로 가지게 된다.

instance variable의 경우에는 객체 하나하나가 생길 때 마다 각자 다른 값을 가지게 된다.

```python
lee = Account('lee')
kim = Account('kim')

lee.name
>'lee'
kim.name
>'kim'
lee.num_accounts
> 2
kim.num_accounts
> 2

```

위 코드의 결과에서 볼 수 있듯이, name 이라는 instance variable은 각 객체마다 따로 값을 가지고 있고, num_accounts라는 class variable은 모든 객체가 공통된 값을 가지고 있는것을 확인할 수 있다.

## 상속

다른 언어와 마찬가지로, python 에서도 상속의 개념이 존재한다.

간단하게 사용법에 대해서만 보자면, 

```python
class Person:
    def eat(self):
        print('eat')
    def sleep(self):
        print('sleep')
```

이런 Person이라는 클래스가 있고, 기본적인 Person 의 기능을 모두 가진 Student 라는 Class 를 만들고 싶다면 다음과 같이 만들면 된다.

```python
class Student(Person):
    def study(self):
        print('study')
```

이렇게 상속을 받게 되면, Student 클래스는 Person 클래스의 모든 성질을 가지게 되는데

```python
lee = Student()
lee.eat()
lee.sleep()
lee.study()
```

이와 같이 Person의 성질을 모두 가지고, Student에 선언한 자신만의 method를 가지게 된다.

## Python Class에서 특별한 method

### init method

Python 의 초기화 method로, 객체가 만들어질 때 자동으로 호출되는 method이다.

객체 생성시에 해야하는 행동이나, 객체 변수들의 초기화에도 사용할 수 있다.

### del method

Python 에서 객체가 소멸할 때 호출되는 method로, init에서는 인자의 변경이 가능했지만 del은 인자의 변경이 불가능하다. 

### repr method

Python print문을 이용하여 출력할 때 출력할 방식을 선언한다.

기존 함수에서 객체의 print 를 하려면 printData() 같은 method를 선언하여 사용하는 방법도 있지만,

간단하게 print문에서 어떻게 동작할지 선언해 줄 수 있다.

### 연산자 중복 method

#### add method

해당 클래스의 객체에서 '+' 연산자의 동작을 정해준다.

이를 연산자 overload라고 하는데, 새로 선언한 class 의 객체인 경우 기본적으로는 '+' 연산자 같은것들이 적용되지 않는다.

#### cmp method

인자로 self, other 두개를 받아서 '=' 연산자의 동작을 정해준다.

