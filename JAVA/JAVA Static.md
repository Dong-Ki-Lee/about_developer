# JAVA Static

static은 보통 변수나 메소드 앞에 static 키워드를 붙여서 사용하게 되는데, 변수 앞에 붙일 때와 메소드 앞에 붙일 때 약간 다른 동작을 하게된다. 이 문서에서는 static의 기본적인 동작에서 부터, 좀 더 심층적인 의미까지 다뤄보고자 한다.



## Static 변수

Java 에서 static 변수란 한마디로 정의하면 다음과 같다.

> 클래스라는 틀을 가지고 만들어진 객체간 공유하는 변수를 가지게 하는 것

항상 정의라고 한문장으로 줄이게 되면 알아듣기가 힘들기 때문에, 좀 더 길게 풀어서 정리하도록 하겠다.

Java 는 객체지향을 기반으로 하는 언어이고, 어떤 문제를 해결할 때 그 문제에 해당하는 것들을 모두 객체화 한다.

class 와 객체의 개념을 잘 모르겠다면 다음을 참고, 아니라면 넘기는 것을 추천한다.

#### Class 와 객체의 차이

예를들어 어떤 학교의 학생들의 점수를 가지고 더하거나 평균을 내거나, 표준편차를 구하는 등의 문제를 해결하기 위한 코딩을 한다면, 각 학생들을 추상화(필요한 특징만을 뽑는 과정)를 거쳐 그들 전체를 대표할 수 있는 어떤 class, 여기서는 student 라는 클래스를 만들었다고 하자. 점수를 다루게 된다면, 각 학생을 구분하는데 학번과 성적이라는 정보만 가지면 될 것이다.

이렇게 모든 학생들을 대표할 수 있는 모습인 student라는 틀을 다음과 같이 만들었다면

```java
public class Student {
    String student_num;
    int score;
    Student(String _student_num, int _score) {
        this.student_num = _student_num;
        this.score = _score;
    }
}
```

각 학생들을 이 틀에 맞춰서 '만들어' 낼 것이다.

```java
public static void main(String[] args) {
    Student s1 = new Student('111111', 50);
    Student s2 = new Student('111112', 60);
}
```

Student 라는 틀에 맞춰 '111111' 학번과 50점의 점수를 가진 s1의 학생과 '111112' 학번과 60점의 점수를 가진 s2라는 학생을 만들었다. 이 각각의 s1, s2라는 학생은, Student 라는 Class형식을 가진 객체가 된다.



#### 그래서 Static 변수란

일반적으로 위처럼 변수를 정의했을 때, 각 객체는 각자의 값을 가지게 된다.

s1이라는 객체가 생성된다면, s1이라는 객체에 string, int 변수가 생성되고, s2 라는 객체가 뒤에 생성된다면, 그 객체에는 또다른 string, int 변수가 생성되는 것이다.

그럴일은 없겠지만, 여기서 한가지 가정을 해보자. 

학교 차원에서 모든 학생이 같은 시간동안 봉사활동을 해서, 같은 봉사활동 시간을 가지는데 이를 저장하고 싶다고 한다면, 기존의 변수를 선언하는 방법으로는 모든 학생들이 다른 봉사활동시간이라는 변수를 가지게 되는데, 이는 다음 두가지의 이유로 효율적이지 못하다.

1. 모두 각자의 변수에 대해 메모리 공간을 할당 받으므로 메모리 사용 측면에서 효율적이지 못하다.
2. 모두 같은 값을 가지게 된다고 가정했을 때, 이 값이 바뀔 경우에 각자 변수를 가지게 된다면 그 모든 각자의 변수를 하나하나 변경해 주어야 한다. 관리 측면에서 이는 효율적이지 못하다.

static 변수는 이럴 때 사용되는 변수인데, static을 사용할 경우 객체는 따로 생성되지만 해당 static 변수는 하나만 생성되어 모든 객체가 그 static 변수 하나를 참고하게 된다.

즉 객체들이 여러개 생성되어도 한번 메모리 공간에 할당된 뒤, 모든 객체가 그 하나의 메모리 공간을 바라보고 있게 된다.

위 점들을 약간 고치면 static 변수를 사용하는 것의 장점이 되는데, 

1. 메모리 할당을 한번만 하게 되어 메모리 사용에 이점을 가지게 된다.
2. 하나의 값을 공유함으로써, 관리가 편해지기도 하고, 공유의 개념을 꼭 사용해야 하는 경우에도 이점을 가진다.



공유의 개념을 사용해야 하는 경우는 다음과 같다.

만약 웹 사이트 방문 조회수를 재는 프로그램을 만들어야 한다면, 

```java
public class Connect {
    String ipAddress;
    static int count = 0;
    Connect(String _ipAddress) {
        this.count++;
        this.ipAddress = _ipAddress;
    }
}
```

이렇게 만든다면, 각 접속에 대한 기록을 남기면서도 조회수 count는 접속 수 만큼 증가할 것이다.



## Static 메소드

보통 유틸리티성 메소드를 작성할 때 많이 사용되는 메소드로, 앞에 static을 붙여서 메소드를 정의하게 되면 클래스를 통해 호출할 수 있게 된다

> 클래스명.메소드명()

따로 클래스를 선언하지 않고도 사용할 수 있는 성질 때문에, 스태틱 메소드 안에서는 일반적인 인스턴스 변수는 접근이 불가능하고, static 변수만 접근이 가능하다.



## Static 을 이용한 Singleton Pattern

Singleton Pattern은 단 하나의 객체만을 생성하도록 강제하는 패턴이다.

먼저 해야 할 일은 생성자를 private로 만드는 것이다.

단 하나의 객체를 생성하기 위해서는 아무곳에서나 생성자를 통해서 생성이 가능하면 안되기 때문이다.

```java
class Singleton {
    private Singleton() {
        
    }
}
```

하지만 위와 같이 하면 생성 자체가 불가능하기 때문에, 생성자는 직접 사용하지 못하지만, 생성자를 호출할 수 있는 static함수를 만들면 다음과 같은 모습이 된다.

```java
class Singleton {
    private Singleton() {
        
    }
    
    public static Singleton getInstance() {
        return new Singleton();
    }
}
```

매번 Singleton의 getInstance() 메소드를 실행하면 생성자를 호출해 반환하게 된다.

그렇지만 이는 호출할 때 마다 새로운 객체를 생성하여 반환하기 때문에 singleton이 아니게 된다.

최종 모습을 보면 다음과 같게 된다.

```java
class Singleton {
    private static Singleton only;
    private Singleton() {
        
    }
    public static Singleton getInstance() {
        if ( only == null ) {
            only = new Singleton();
        }
        return only;
    }
}
```

이런식으로 코드를 구성하면 singleton pattern에 맞춰 하나의 객체만 생성되는 코드가 된다.



## Java에서 static 사용을 지양해야 하는 이유

Static 변수는 global state를 상징하는데, global state는 추론하고 테스트 하는 데 어디서 변경이 될 지 모르기 때문에 추론과 테스트가 매우 까다롭다. 작은 규모의 시스템에는 상관이 없겠지만, 백만줄이 넘어가는 대규모 시스템의 경우 global state의 추론이 굉장히 어려워지기 때문에 모듈화가 제대로 이뤄지지 않는다

좀 더 정리해서, 다음과 같은 이유로 Java에서 static 사용을 지양해야 한다

1. static은 객체지향의 방향에 어긋난다.

* 각 객체의 데이터들이 캡슐화 되어있어야 한다는 원칙에 위반
* 스코프를 고려할 필요가 없는 절차지향에 가깝게 된다.

2. Interface 를 구현하는데 사용될 수 없다. ( 재사용성이 떨어짐 )
3. static 변수는 프로그램이 실행되면 GC에 의해서 회수되지 않게 되기 때문에 메모리에 악영향을 미칠 수 있다.

