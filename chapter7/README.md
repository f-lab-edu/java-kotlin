# 요약

## 7장. 비용 줄이기

## 아이템 45. 불필요한 객체 생성을 피하라

- 객체를 Wrap 하게 되면 3가지 비용이 발생한다.
    - 헤더 및 레퍼런스를 위한 추가 공간
    - 요소가 캡슐화 되어있다면, 접근을 위한 함수 호출 비용
    - 객체 생성을 위한 메모리 공간 할당 및 레퍼런스 생성 비용
- 캐싱 기법을 활용해서 객체를 재활용하면 불필요한 객체 생성으로 인한 비용을 줄일 수 있다.
    - 단, 캐시는 언제나 메모리와 성능의 트레이드 오프가 발생하기 때문에 여러가지 상황을 잘 고려해서 사용해야한다.
- 무거운 클래스를 생성할 때 지연 초기화를 하는 것이 좋을 수 있다.
    - 하지만, 백엔드 애플리케이션과 같은 특수한 경우에는 지연초기화를 통해 첫번째 응답시간이 굉장히 길어지는 문제와 성능 테스트가 복잡해지는 단점을 가지고 있다.

## 아이템 46. 함수 타입 파라미터를 갖는 함수에 inline 한정자를 붙여라

- `inline` 한정자의 역할은 컴파일 시점에 함수를 호출하는 부분을 함수의 본문으로 대체하는 것이다.
    - 일반적인 함수를 호출하면 함수 본문으로 점프하고 본문의 모든 문장을 호출한 다음, 함수를 호출했던 위치로 다시 점프하는 과정을 거친다.
    - `inline` 한정자를 사용하면 이러한 점프가 일어나지 않는다.
- `inline` 한정자를 사용하면 다음과 같은 장점을 얻을 수 있다.
    - 타입 아규먼트에 `reified` 한정자를 붙여서 사용할 수 있다.
    - 함수 타입 파라미터를 가진 함수가 훨씬 더 빠르게 동작한다.
    - 비지역 리턴을 사용할 수 있다.
- `inline` 한정자는 모든 곳에서 사용할 수 없다.
    - 재귀적으로 사용할 경우 무한하게 대체되는 문제가 발생한다.
    - 가시성 제한을 가진 요소를 사용할 수 없다.
    - `inline` 한정자를 남용하면 코드의 크기가 쉽게 커진다.
- `crossinline` : 아규먼트로 인라인 함수를 받지만 비지역적 리턴을 하는 함수는 받을 수 없게 만든다.
    - 인라인으로 만들지 않은 다른 람다 표현식과 조합해서 사용할 때 문제가 발생하는 경우에서 활용한다.
- `noninline` : 아규먼트로 인라인 함수를 받을 수 없게 만든다, 인라인 함수가 아닌 함수를 아규먼트로 사용하고 싶을 때 활용한다.

## 아이템 47. 인라인 클래스의 사용을 고려하라

- 프로퍼티가 단 하나만 존재하는 클래스는 `inline` 한정자를 붙여서 `inline` 클래스로 만들 수 있다.
    - `inline` 클래스는 해당 객체를 사용하는 위치가 모두 해당 프로퍼티로 교체된다.
    - `inline` 클래스의 메서드는 모두 정적 메서드로 만들어진다.
- `inline` 클래스는 다른 자료형을 Wrapping해서 새로운 자료형을 만들 때 많이 사용된다.
- `inline` 클래스도 인터페이스를 구현할 수 있지만, 인터페이스를 구현하는 `inline` 클래스는 `inline` 으로 동작하지 않는다.
    - 인터페이스를 통해서 타입을 나타내려면, 객체를 Wrapping해서 사용해야하기 때문에 인터페이스를 구현하는 `inline` 클래스는 아무런 의미가 없다.
- `typealias` 를 이용해서 타입에 새로운 이름을 붙여줄 수 있으며, 이는 길고 반복적으로 사용해야할 때 유용하다.
    - `typealias` 는 단순하지만 안전하지 않으며, 이를 잘못 사용한 경우에도 어떠한 요류가 발생하지 않기 때문에 문제를 찾는 것을 더 어렵게 만든다.
    - 때문에 비용과 안전이라는 두 가지 측면을 위해서는 `inline` 클래스를 사용하자.

## 아이템 48. 더 이상 사용하지 않는 객체의 레퍼런스를 제거하라

- 가비지 컬렉터를 맹신하고 메모리 관리를 완전히 무시해버리면, 메모리 누수가 발생하여 최악의 경우 OOME가 발생할  수 있다.
    - 때문에 더 이상 사용하지 않는 개체의 레퍼런스는 유지하면 안된다라는 규칙 정도는 지켜주는 것이 좋다.
- 객체에 대한 참조를 `companion` 또는 `static` 으로 유지해버리면, 가비지 컬렉터가 해당 객체에 대한 메모리 해제를 할 수 없다.
    - 특히, Activity와 같은 큰 객체를 이렇게 선언할 경우 메모리를 해제할 수 없어 굉장히 큰 메모리 누수가 발생하게 된다.
    - 때문에 비용이 큰 객체는 리소스를 정적으로 유지하지 않는 것이 가장 좋다.
- 범용적으로 사용하는 라이브러리는 어떻게 사용될지 예측하기 어렵기 때문에 최적화에 신경을 더 써야한다.
    - 때문에 사용하지 않는 오브젝트에 명시적으로 `null` 을 할당하여 초기화하자.

# 개인 독후감

## Charles
 내가 Kotlin을 공부하던 당시에는 inline class가 없던 때였는데 이번에 책을 통해 알게
되었다. 의도를 표현하기 위해 typealias를 자주 사용했었는데, 코드에 inline class를
적용해보았다. typealias를 나도 모르게 원래의 클래스로 변환해서 사용한 곳이 많았다.
이로 인해 번거로움이 컸다. 애초에 엄격하게 적용하지 않은 나의 잘못이고, 일단 적용한
후에 타입 시스템의 도움을 받을 것을 기대한다.
 하지만, 원 타입의 메쏘드가 모두 사리지면서 delegation 메쏘드를 작성해야 해서 매우
번거로왔다. 간단히 List에 대한 inline class로 FruitList를 만든다면, 모든 리스트의
메쏘드를 작성해야 한다.
 또 다른 문제점은 값은 전환시 typealias 보다 번거롭다는 점이다. 팩토리 메쏘드를
사용하면 그나마 낫기는 하다. 어쨋든 typealias와 비교하기에는 여러모로 차이가 있고
wrapper클래스의 비용을 제거하는데 목적이 있다. 처음보는 개념이라 좀 더 찾아보았는데
책의 내용이 최신 정보가 아니라 Deprecated된 정보를 담고 있다. 책보다는 링크를
참조하기 하는 것이 좋을 것 같다.

- https://kotlinlang.org/docs/inline-classes.html
- https://github.com/Kotlin/KEEP/blob/master/notes/value-classes.md
- https://github.com/Kotlin/KEEP/blob/master/proposals/inline-classes.md

## Kuma
이번 장에선 이론적으로 반대할 얘기는 없었다. 실생활에서도 비용을 줄이려면 지출을 줄이거나
최대한 할인, 포인트를 사용해 값을 줄이는 것처럼, jvm이 조금이라도 덜 가동되도록
머리를 굴려 프로그래밍을 짜야하겠지. 수동으로 객체를 해제시키는 방법은 자세히 읽게 되었다. 
jvm 내 gc의 존재는 우리가 메모리 관리에 대해 한없이 느슨해지면서 
우리가 적극적으로 튜닝하려 나서면 안 되는 존으로 인식을 주었기 때문이다. 하지만 관여를 하면 
안되는 거지, 메모리 누수를 막기 위해 우리가 최선을 다해 코드를 짜야한다는 걸 다시 리마인드
시켜주었다.(지금까지 막 짠 내 코드가 생각나며 jvm에게 사과하게 되는 순간이었다.)
인라인 클래스는.. 아직 감이 안 온다. 저자가 굉장히 어필하는 기능인데 장단점을 써놓은 걸 보니
상황에 따라 조심해서 써야하는 기능처럼 보였다. 더 알아보려 검색을 해보니 inline modifier가
1.5.0에선 deprecated 됐다. 음.. 책 출판 2년 후에 deprecated 된 거니 어쩔 수 없겠지.
역시 책은 책이고, 팩트 체크는 독자의 몫이다.

## Olive
사실 책의 초반에도 나와있듯이 "오늘날에는 코드의 효율성을 관대하게 바라본다."는 것에 공감하고, 나 조차도 코드를 작성할 때 코드의 효율성 보다는 가독성이나 다른 가치들에 좀 더 
집중하는 것 같다. 하지만 JVM 환경에서의 메모리 누수로 인한 OOME는 언제나 크리티컬한 이슈이다. 대부분의 OOME 이슈는 이렇게 사소한 부분들이 점차 쌓이고 쌓여서 만들어진다고 생각하는데, 
아무리 하드웨어가 비약적으로 발전하고 JVM의 성능이 좋아졌지만 이것이 만능은 아니기 때문에 언제나 개발자는 이러한 부분들을 꼼꼼하게 신경써야하는 것 같고, 특히 책에서 언급한 몇가지 주의점들을 통해 적은 비용으로 최적화 할 수 있는 부분들은 훌륭한 예방법인 것 같다. 책의 후반부에는 `inline` 한정자에 대한 내용이 나오는데, NextStep을 수강할 때는 `inline` 클래스가 아닌 `value` 클래스로 사용했던 것 같다. (지금에서야 다른 분들의 리뷰를 보고 해당 키워드가 `deprecated` 되었다는 것을 알게 되었다.), 사실상 그 때는 `value` 클래스를 사용하면서도 이유를 잘 모르고 왜 `data` 클래스가 아닌 `value`를 사용하지 거의 둘다 비슷한것 아닌가, Wrapper 클래스나 단일 프로퍼티를 가진 값 객체를 정의할 때 `value` 클래스를 사용하나보다라고 생각했는데, 지금 생각해보니 `value` 클래스가 제공해주는 여러 기능들과 제약사항 이외에도 비용 최적화 측면에서의 가치에 대해서 한번더 생각해보게 되었다. 

# 토론 주제 

