# JAVA Exception

## Error 와 Exception의 차이

* Error 는 시스템에 비정상적인 이상이 생겼을 때 생기는 것으로 프로그래머가 미리 예측하여 처리할 수 없다. 어플리케이션을 제작할 때 처리를 신경쓰지 않아도 된다.
* Exception 은 어플리케이션 로직상에서 발생하는 것으로, 발생할 상황을 예측하고 처리하는 것이 가능하다. 어플리케이션을 제작할 때 Exception을 구분하고 그에따른 처리를 해야한다.

## Exception 클래스 구조

Exception 의 상속 구조는 다음과 같다.

> Object -> Throwable -> Eception

Throwable을 상속받는 클래스는 Error와 Exception이 있고, Exception클래스를 여러 Exception들이 상속받게 된다.

## Checked Exception VS Unchecked(Runtime) Exception

Exception 은 두종류로 나뉘게 되는데, Checked Exception과 Unchecked Exception이 그것이다.

여러 항목으로 이 둘의 차이점을 알아보면 다음과 같다.

1. 이 둘을 명확히 구분하자면, '꼭 처리를 해야하는가' 가 기준이 되는데, Checked Exception의 경우엔 Exception이 발생할 가능성이 있는 메소드에서는 반드시 try/catch나 throw로 처리해야하는데 Unchecked Exception은 명시적인 예외처리를 하지 않아도 된다는 점이 구분할 수 있는 차이점이 된다.
2. Unchecked Exception은 모두 Runtime Exception의 하위 Exception들인데, Runtime 이라는 이름으로 알 수 있듯 컴파일 단계에서는 알 수 없고 실행과정 중에 발생한다고 해서 Runtime Exception이라고 한다. Checked Exception의 경우 컴파일 단계에서 체크가 가능한 Exception이다.
3. Checked Exception 의 경우 예외가 발생하면 transaction 의 roll-back 없이 exception을 일으키지만, Unchecked Exception은 예외 발생시 transaction의 roll-back이 일어난다는 것의 차이가 있다.