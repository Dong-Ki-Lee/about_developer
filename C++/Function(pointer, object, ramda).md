# 함수 포인터, 함수 객체, 람다

STL과 같은 라이브러리에서 가장 중요한 점을 두개 생각한다면 범용성과 효율성이 될 것이다.

어디에 사용하든 사용이 용이해야하고, 최적화가 잘 되어있어야 한다는 말이다.

이런 부분에 관련해서 설명하기 위한 기본 개념들을 먼저 설명하고자 한다.

## 함수 포인터

포인터는 해당 객체의 주소를 가리키는 값이다. 함수에도 이런 포인터가 존재하는데, 이말인 즉슨 함수에도 주소가 존재한다는 것이다. 함수명은 함수의 시작 주소가 되고, 함수의 원형과 같도록 선언하는 것으로 함수의 포인터를 선언할 수 있다.

```c++
int sum(int a, int b); //이런 함수가 존재할 때
int (*pf)(int, int) = sum; //이런 형식으로 함수의 포인터를 선언할 수 있다.
```

함수의 원형이 같도록 선언한다는 말을 좀 더 쉽게 말하면, 함수의 인자로 들어가는 값을 위 선언과 같이 같게 만들어 줘야 한다는 것이다.

이런 함수 포인터 pf를 가지고, 함수 sum을 사용하는 것과 동일하게 사용할 수 있다.

```c++
#include <iostream>
using namespace std;

int sum(int a, int b) {
    return a + b;
}

int main() {
    int (*pf)(int, int) = sum;
    
    cout << pf(4,5) << endl;
}
```

이런식으로 함수포인터를 함수처럼 사용할 수 있고, 

```c++
cout << pf << endl;
cout << sum << endl;
```

이렇게 출력하면 같은 주소값을 가리키고 있는 것을 확인할 수 있다.

## 맴버 함수 포인터

맴버 함수란 클래스 내부에 있는 함수로, 클래스의 맴버로 있는 함수를 의미한다. 

맴버 함수는 함수 포인터를 선언하는 방식이 약간 다르다.

Rectangle 클래스에서 area라는 함수가 있을 때, 원형을 다음과 같다고 생각해보자.

```c++
int Rectangle::area(int width, int height)
```

이 함수에 대해 함수 포인터를 선언하는것은 다음과 같이 가능하다.

```c++
int (Rectangle::*pf)(int, int) = &Rectangle::area;
```

예제를 통해서 좀 더 알아보자

```c++
#include <iostream>
using namespace std;

class Rectangle {
    int width;
    int height;
    public:
    explicit Rectangle(int _width = 0, int _height = 0) : width(_width), height(_height) {}
    int area() {
        return width * height;
    }
}

int main() {
    Rectangle rc(10, 5);
    int (Rectangle::*pf)(void) = &Rectangle::area;
    
    cout << (rc.*pf)() << endl;
    return 0;
}
```

함수 포인터 pf가 Rectangle 의 area 맴버 변수의 시작주소를 가지게 하고, 함수 포인터로 실제 함수를 호출하려면 .* 연산자를 이용한다.