# STL Algorithm

이번에는 STL Algorithm에 대해서 다루고자 한다.

STL Algorithm은 크게 네 가지로 분류할 수 있다.

* 변경 불가 시퀀스 알고리즘
  * 대상 컨테이너의 내용을 변경하지 않는 알고리즘. find, for_each등이 있다.
* 변경 가능 시퀀스 알고리즘
  * 대상 컨테이너의 내용을 변경하는 알고리즘. copy, generate등이 있다.
* 정렬 관련 알고리즘
  * 정렬이나 합하는 알고리즘이 있다. sort, merge등이 있다.
* 범용 수치 알고리즘
  * 값을 계산하는 알고리즘으로 accumulate 등이 있다.

## 변경 불가 시퀀스 알고리즘

### find

컨테이너에 있는 데이터 중 원하는 것을 찾기위한 알고리즘이 find 알고리즘이다.

#### find 의 원형

```c++
InputIterator find( InputIterator _First, InputIterator _Last, const Type& _Val );
```

첫번 째 parameter는 찾기 시작할 반복자의 위치, 두번 째 parameter는 마지막 위치, 세번 째 parameter는 찾을 값

찾는 값이 있을 경우 데이터가 있는 위치를 가리키는 Iterator를 반환하고, 실패하면 반복자의 end()를 반환한다.

실제 코드를 통해 설명한다.

#### find 사용 코드

```c++
#include <iostream>
#include <algorithm>
#include <vector>

using namespace std;

int main() {
    vector<int> Codes;
    Codes.push_back(33);
    Codes.push_back(55);
    Codes.push_back(77);
    
   	vector<int>::iterator FindIter;
    
    FindIter = find(Codes.begin(), Codes.end(), 55);
    
    if( FindIter != Codes.end() ) {
        //있을 때
    } else {
        //없을 때
    }
    
    return 0;
}
```

### find_if

find는 컨테이너가 기본형을 저장하고 있을 때만 사용할 수 있다. 유저가 정의한 정의형을 저장하는 컨테이너는 find를 사용할 수 없다. find_if는 이를 조건자를 받아 유저가 정의한 정의형도 처리할 수 있는 find이다.

좀 더 간단히 설명하자면, 기본형에 대한 비교방법은 이미 모두 정의가 되어있다. 예를들어, 정수와 정수를 비교할 때 <, > 같은 연산자를 이용하여 10 < 20 같은 비교가 가능하다. 하지만 사용자가 정의한 structure라면, 다음의 예를 보자.

```c++
struct Human {
    int weight;
    string name;
}
```

이런 구조체가 선언되었을 때, Human 구조체에 대한 비교는 어떤 방식으로 진행할 것인가. 이를 정해주지 않는다면 연산하는 방법을 모르기 때문에 연산이 안되는 것이다. 즉, 연산하는 방법에 대해 알려준다면 기존의 알고리즘을 사용할 수 있다.

만일 여기서 Human을 계산하는 방법을, <, >, == 연산자에 대해 weight를 비교한다는 사실을 명시하여 find_if 에게 전해준다면, 이것은 find의 역할을 해낼 것이다.

#### find_if 의 원형

```c++
InputIterator find_if( InputIterator _First, InputIterator _Last, Predicate _Pred );
```

find와 비교하면, 세번째 parameter가 다르다. find 에서는 찾을 값을 넣었지만, 여기에서는 조건자를 넘기게 된다.

#### find_if 사용 코드

```c++
#include <iostream>
#include <algorithm>
#include <vector>

using namespace std;

struct Human {
    int weight;
    string name;
}

// 조건자
struct FindWeightHuman {
    bool operator() (Human& human) const {
        return human.weight == CompareWeight;
    }
    int CompareWeight;
}

int main() {
    vector<Human> humans;
    
    Human human1;
    human1.weight = 55;
    human1.name = 'lee';
    
    Human human2;
    human2.weight = 77;
    human2.name = 'kim';
    
    humans.push_back(human1);
    humans.push_back(human2);
    
    vector<Human>::Iterator FindHuman;
    
    FindWeightHuman sFindWeightHuman;
    sFindWeightHuman = 55;
    
    FindHuman = find_if(humans.begin(), humans.end(), tFindWeightHuman);
    
    if(FindHuman != humans.end()) {
        //존재할 때
    } else {
        //존재하지 않을 때
    }
    
    return 0;
}
```

### for_each

for_each는 컨테이너에 있는 데이터들을 차례로 넣으면서 함수를 실행시키는 알고리즘이다.

특정 컨테이너 객체 그룹에 대해 어떤 함수를 실행시켜야 하는 경우와 같은때에 이용한다.

#### for_each 의 원형

```c++
Fucntion for_each(InputIterator _First, InputIterator _List, Function _Func);
```

첫 번째와 두 번째 parameter로 시작위치와 끝위치를 알려주고, 세 번째 parameter로는 이를 parameter로 받아서 실행할 함수가 들어간다.

#### for_each 사용 코드

```c++
#include <iostream>
#include <algorithm>
#include <vector>

using namespace std;

struct Human {
    int age;
    string name;
};

struct UpdateAge {
    void operator() (Human& human) {
        human.age += 1
    }
};

int main() {
    vector<Human> humans;
    
    Human human1;
    human1.age = 20;
    human1.name = "lee";
    Human human2;
    human2.age = 30;
    human2.name = "kim";
    
    humans.push_back(human1);
    humans.push_back(human2);
    
    UpdateAge = updateAge;
    
    for_each(humans.begin(), humans.end(), updateAge);
    
    return 0;
}
```

