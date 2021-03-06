# 요약
## 4장. 추상화 설계

- 추상화는 복잡한 자료, 모듈, 시스템 등으로부터 핵심적인 개념 또는 기능을 간추려내는 것을 의미한다.
- 조금 간단히 표현하면, 추상화는 복잡성을 숨기기 위해 사용되는 단순한 형식을 의미한다.
    - ex. 인터페이스 → 클래스라는 복잡한 것에서 메서드와 프로퍼티만 추출해서 간단하게 만들었기 때문에 클래스에 대한 추상화로 볼 수 있다.
- 객체는 여러 형태로 추상화해서 표현할 수 있으며, 추상화를 위해서 객체에서 무엇을 감추고 노출해야하는지를 결정해야한다.

### 프로그래밍에서의 추상화

- 모듈, 라이브러리 등으로 분리한다는 의미가 아닌, 함수를 정의할 때 구현을 함수 시그니처 뒤에 숨기게 되는 것을 추상화라고 한다.

### 추상화와 자동차

- 자동차를 운전할 때 운전자는 자동차의 내부 요소들을 실시간으로 이해하고 조정해야할 필요없이, 자동차를 조종하는 인터페이스의 사용방법만 알면된다.
- 자동차의 내부 구조가 바뀌거나, 특수한 시스템을 도입하더라도 인터페이스는 거의 동일하게 유지된다.
- 여기서 중요한 것은, 운전자는 자동차가 어떻게 바뀌던 상관없이 동일한 인터페이스로 운전할 수 있다는 것이다.
- 추상화는 내부적으로 일어나는 모든 것들을 마법처럼 숨겨준다.

프로그래밍에서는 다음과 같은 목적으로 추상화를 해야한다.

- 복잡성을 숨기기 위해서
- 코드를 체계화 하기 위해서
- 만드는 사람에게 변화의 자유를 주기 위해서

## 아이템 26. 함수 내부의 추상화 레벨을 통일하라

- 계층이 잘 분리된다면, 다른 계층은 이미 잘 완성되어있기 때문에, 고려할 필요없이 해당 계층만 생각하면 된다. (전체를 이해할 필요가 없어진다.)
- 추상화 레벨이 높을 수록 걱정해야하는 세부적인 내용들이 적어지고, 단순함을 얻지만, 제어력을 잃는다.
- 코드 또한 추상화를 계층처럼 만들어서 사용할 수 있으며 이를 위한 가장 기본적인 도구가 함수이다.
    - 함수도 높은 레벨과 낮을 레벨을 구분해서 사용해야한다. (Single Level of Abstraction, SLA)

### 거대한 함수의 문제점

- 너무 많은 로직을 수행하는 거대한 함수의 문제점
    - 읽으면서 세부적인 내용을 하나하나 신경써야하기 때문에 읽고 이해하는 것이 거의 불가능에 가깝다.
    - 요구사항에 따라 어떤 부분을 어떻게 수정해야할지 막막하다.
- 함수를 여러 하위 계층의 함수로 나누어 구성하는 경우의 장점
    - 함수가 어떤식으로 동작하는지 이해하기 쉽다.
    - 하위 계층의 함수를 이해하기 위해서는 해당 부분의 코드만 살펴보면 된다.
    - 메서드 추상화를 통해 가독성을 크게 향상시킬 수 있다.
    - 함수를 구성하는 더 작은 단위의 함수로 추출하면 재사용과 테스트가 쉬워진다.

### 함수는 간단해야 한다

- 함수는 작아야하며, 최소한의 책임만을 가져야한다.
- 어떤 함수가 다른 함수보다 복잡하다면 일부분을 추출해서 추상화하는 것이 좋다.

### 프로그램 아키텍처 추상 레벨

- 추상화를 구분하는 이유는 서브 시스템의 세부 사항을 숨김으로써 상호 운영성과 플랫폼 독립성을 얻기 위함이다. (이는, 문제 중심으로 프로그래밍 한다는 의미)
- 이러한 개념은 모듈 시스템을 설계할 때도 중요하며, 모듈 시스템을 계층 단위로 분리함으로써 계층 고유 요소를 숨길 수 있다.
    - ex. 애플리케이션을 만들 때, 입 출력을 위한 모듈과 비즈니스 로직을 위한 모듈을 나눌 수 있다.
- 계층화가 잘 된 프로젝트는 어떤 계층 위치에서 코드를 보아도 일관적인 관점을 얻을 수 있다.

## 아이템 27. 변화로부터 코드를 보호하려면 추상화를 사용하라

> 물 위를 걷는 것과 명세서로 소프트웨어를 개발하는 것은 둘다 쉽다. 둘 다 동결되어 있다면...
> 
- 함수와 클래스 등의 추상화로 실질적인 코드를 숨기면, 사용자가 세부 사항을 알지 못해도 괜찮다는 장점이 있다.
    - ex. 정렬 알고리즘을 함수로 추출하고 함수 시그니처를 사용자 공개 API로 제공하면, 이를 사용하는 코드에 어떠한 영향을 주지 않고 성능을 최적화 할 수 있다.
- 추상화를 통해 변화로 부터 코드를 보호하는 방법
    - 상수
        - 반복 사용되는 리터럴을 상수 프로퍼티로 추상화하면, 이름을 붙일 수 있고 나중에 변경에 쉽게 대응할 수 있다는 장점이 있다.
    - 함수
        - 함수는 추상화를 표현하는 수단 중 하나이며, 함수 시그니처는 함수가 어떤 추상화를 표현하고 있는지 알려준다.
        - 함수는 매우 단순한 추상화 수단이지만 상태를 유지하지 않고, 함수 시그니처를 변경함에 따라 이에 의존적인 많은 부분에 큰 영향을 줄 수 있다는 제한 사항이 존재한다.
    - 클래스
        - 클래스는 함수보다 구현을 추상화 할 수 있는  강력한 방법으로 상태와 많은 함수들을 가질 수 있다.
        - 클래스는 훨씬 더 많은 자유를 보장해주지만, 여전히 한계가 존재한다.
    - 인터페이스
        - 코틀린의 표준 라이브러리의 거의 모든 것이 인터페이스로 표현된다.
        - 라이브러리를 만드는 사람들은 내부 클래스의 가시성을 제한하고, 인터페이스를 통해 이를 노출하는 코드를 작성하는데, 이렇게하면 사용자가 클래스를 직접 사용하지 못하기 때문에 라이브러리를 만드는 사람들은 인터페이스만 유지한다면, 원하는 형태로 구현을 변경할 수 있다.
        - 인터페이스를 이용해서 클래스를 숨기게되면 더 많은 자유를 얻을 수 있다. (변화에 대한)
    - Wrapper 클래스
        - 보편적인 객체를 특수한 객체로 래핑하여 내부 구현을 숨김으로써, 변화에 좀 더 자유로운 구조를 만들 수 있다.
- 추상화는 이처럼 많은 자유를 보장하지만, 코드를 이해하고 수정하기 어렵게 만든다.
    - ex. FizzBuzz Enterprise Edition 프로젝트를 같이 과도한 추상화는 오히려 소프트웨어 복잡성을 높이고 유지보수를 힘들게 만들 뿐이다. (뭐든지 극단적이게 되지 말자)

## 추상화와 균형

- 추상화를 통해 많은 것을 숨기고 복잡성을 단순화 할 수 있지만, 너무 숨기게 되면 오히려 결과를 이해하기 어렵게 만들고 구조의 복잡성을 높이게 된다.
- 추상화의 적절한 균형을 찾는 것은, 팀의 크기, 경험, 프로젝트의 크기, 특징, 도메인 지식 등에 의해 달라질 수 있으며, 많은 시간과 경험이 필요하다.
- 소프트웨어 세계는 항상 변화한다. (소프트웨어의 핵심 가치는 변화), 변화에 유연하게 대처할 수 있는 구조를 설계하는 것도 중요하지만, 뭐든지 너무 과해서는 안된다. (너무나도 먼 미래의 극단적이고, 낮은 확률의 변화 가능성까지 고려하여 설계하는 것은 오버엔지니어링이 될 수 있다고 생각)

> 추상화는 단순하게 중복성을 제거하기 위해 코드를 구성하기 위한 것이 아니다. 추상화를 사용하는 것은 굉장히 어렵지만, 코드를 변경하고 유지보수할 때 큰 도움이 된다.
추상화의 장점과 단점 사이의 적절한 균형을 찾는 것이 중요하다.
> 

## 아이템 28. API 안정성을 확인하라

- 인터페이스는 안정적이면서 표준적인 것이 좋다.
    - API가 변경된다면, 해당 API에 의존적인 많은 부분에 문제가 발생한다.
    - 사용자가 새로운 API를 배우기 위해서 많은 리소스를 투자해야한다.
- 처음부터 좋은 API를 설계하는 것은 불가능하며, API를 개선하기 위한 변경과 API를 안정적으로 유지하기 사이의 적절한 균형을 유지해야한다.
    - API가 불안정하다면 이를 명확하게 알려주어야하며, 버저닝 시스템을 통해 안정성을 가시적으로 나타낼 수 있다.
    - 안정적인 API와 안정적이지 않은 부분에 대한 브랜치를 별도로 운영한다.
    - @Experimental 등의 메타 어노테이션을  이용해서 해당 요소가 명시적으로 불완전함을 나타낼 수 있다.
    - 안정적인 API 일부를 변경해야한다면, 전환하는데 시간을 두고 @Deprecated 어노테이션을 활용해서 사용자에게 미리 알려줘야한다.

## 아이템 29. 외부 API를 Wrap 해서 사용하라

- 클라이언트가 API를 신뢰할 수 없다면 해당 API는 불안정한 것이다.
- 불안정한 API를 과도하게 사용하는 것은 위험하며, 어쩔 수 없이 사용해야하는 경우에는 API를 로직과 직접적으로 결합시키지 않는 것이 좋다.
- 때문에, 불안정하다고 판단되는 외부 API를 Wrap해서 사용하면 자유와 안정성을 얻을 수 있다.
    - 문제가 발생한 경우 Wrapper만 변경하면되기 때문에, 변경에 쉽게 대응할 수 있다.
    - 프로젝트의 스타일에 맞춰서 API의 형태를 조정할 수 있다.
    - 필요한 경우 쉽게 동작을 추가 및 수정할 수 있다.

## 아이템 30. 요소의 가시성을 최소화하라

- API를 설계할 때 가능한 간결한 API를 선호하는데에는 여러가지 이유가 존재한다.
    - 작은 인터베이스는 배우기 쉽고 유지보수하기 쉽다.
    - 변경을 가할 때는 기존의 것을 감추는 것보다 새로운 것을 노출하는 것이 쉬우며, 공개적으로 노출된 API가 많다는 것은 그만큼 변경이 힘들다는 것을 의미한다.
- 클래스의 상태를 나타내는 프로퍼티를 외부에서 변경할 수 있다면, 클래스는 자신의 상태를 보장할 수 없으며, 불변성을 해친다.
    - 이것은 단순히 외부에서 상태를 변경한다는 것으로 그치는게 아니라, 예상치 못한 변경에 의해서 예외가 발생하고 코드의 신뢰성 저하로 이어질 수 있다.
    - 가시성이 제한되지 않은 경우 변경을 트래킹하기 어려우며, 프로퍼티의 상태를 이해하기 어렵다.
    - 쓰레드 세이프하지 않기 때문에 병렬 프로그래밍할 때에 어려움이 있다.
- 내부적인 변경 없이 작은 인터페이스를 유지하고 싶다면, 가시성을 제한하라.

## 아이템 31. 문서로 규약을 정의하라

- 일반적으로 대부분의 함수와 클래스는 이름만으로 예측할 수 없는 세부사항들을 가지고 있다.
    - ex. 책에서 설명하고 있는 멱집합 함수의 예시
- 행위가 문서화되지 않고, 요소의 이름이 명확하지 않다면 이를 사용하는 사용자가 현재 구현에만 의존하게 된다.

## 규약

- 어떤 행위를 설명하면 사용자는 이를 일종의 약속으로 취급하고, 이를 기반으로 스스로 자유롭게 생각하던 예측을 조정한다.
- 이러한 예측되는 행위를 요소의 규약이라고 부른다.
- 규약을 정의하게되면, 클래스를 설계하고 사용하는 사람 모두에게 좋은일이다.
    - 클래스를 설계하는 사람은 클래스가 어떻게 사용될지 (작성자의 의도에 맞게 사용될지) 걱정하지 않아도되며
    - 클래스를 사용하는 사람은 내부적으로 어떻게 구현되어있는지 걱정할 필요가 없다
- 이름, 주석과 문서, 타입을 통해 규약을 정의할 수 있다.
- 규약에서 중요한 것은, 단순한 합의를 이를 만들고 사용하는 양쪽 모두 존중해야함에 있다.

> 주석을 반드시 달아야 하는가?
> 

## 타입 시스템과 예측

- 타입 계층은 객체와 관련된 중요한 정보로, 인터페이스는 우리가 구현해야한다고 약속한 메서드 목록 이상의 의미를 갖는다.
- 클래스와 인터페이스에도 여러가지 예측이 들어가며, 클래스가 어떠한 동작을 수행할 것이라고 예측되면 서브 클래스도 이를 보장해야한다. (ISP)
    - 만약 클래스가 어떻게 동작할 것이라는 예측 자체에 문제가 있다면 클래스와 관련된 다양한 상속 문제가 발생할 수 있다.
- 때문에, 사용자가 클래스의 동작을 확실하게 예측할 수 있게 하려면 공개된 API에 대해서 규약을 잘 정의해야한다.
    - 이러한 규약은 대체로 문서를 통해 전달되어진다.
- 구현의 세부사항을 달라질 수 있지만, 캡슐화를 통해 이를 보호하고 제어할 수 있다.

## 아이템 32. 추상화 규약을 지켜라

- 규약은 단순한 합의이기 때문에 때로는 한쪽에서 규약을 위반할 수 있다.
    - ex. 리플렉션을 이용한 규약의 위반
- 규약을 위반하는 것은 잠재적인 문제를 수반하기 때문에 규약을 깰 수밖에 없는 상황이라면 이를 잘 문서화해서 공유하는 것이 중요하다.


# 개인 독후감

## Charles
### 느낀 점

 이번 추상화를 다룬 장은 매우 만족스러웠다. 나는 추상화 능력을 매우 중요하게
생각한다. 유발 하라리는 저서 "사피엔스"에서 허구를 말할 수 있는 능력을 통해 수억 명의
사람들이 협력할 수 있었다고 했다. 공학 관점에서 추상화라는 것은 인간의 커뮤니케이션의
복잡성 문제를 해결한다. 물론 커뮤니케이션 관점외에다 많은 장점을 가지고 있다. 이처럼
추상화 능력은 문제 해결 능력에 아주 많은 부분을 차지한다고 할 수 있다.
 멘토링 과정에서도 프로젝트를 시작하면 아주 오랜 기간을 프로토타입 기간을 거치도록
한다. 이 과정에서 추상화를 위한 훈련을 시킨다. 물론 높은 수준까지는 다다르지 못하지만
처음보다는 많이 좋아지는 경우가 다수이다. 개인마다 다르지만 추상화 능력을 가지고 있는
개발자는 프로그래밍에서의 추상화도 쉽게 적응한다. 반대로 프로그래밍에서의 추상화를
훈련하면서 추상화하여 사고하는 능력을 발전시킨다. 개발자 뿐만 아니라 문제 해결 능력을
필요로 하는 모든 이에게 있어 추상화는 꼭 필요한 요소이다.
 책의 성격상 어쩔 수 없는 부분이기는 하지만 추상화의 방향과 훈련법을 몇가지 제시해 
주었으면 더 좋았을 것 같다. 사람마다 배경 지식이 달라 일반화하기 어렵더라도 처음
코틀린을 배우는 함수형 프로그래머 정도로 상정하여 제시하였다면 어땠을까 싶다.

## Taek
### 느낀 점

  추상화 기법은 Spring 프레임워크로 개발할 때 지겹도록 들어서 중요성에 대해서는 익히 알고있다.
  이번 장에서는 단순 추상화의 좋은 점과 코틀린에서 어떻게 사용해야 하는지를 안내하고 있다. 
  인상 깊게 봤던 Item은 소프트웨어 공학에서 말하고 있는 추상화 레벨과 프로그램 아키텍처의 추상 레벨이다.
  그 외에 재사용장에서도 말했던 무조건 추상화를 많이 하는 것보다 적절한 추상화 적용을 안내하고 있다.
  재사용성과 마찬가지로 추상화 또한, 단순 반복적인 코드 레벨을 줄이고, 하나의 레고 부품처럼 나타내 활용하는 것으로 이해했는데
  공학적인 관점에서의 추상화와 실제 세계에서의 추상화를 비교하여 코드를 체계화해야겠다고 느꼈다.

## KUMA
### 느낀 점
이번 장은 읽는게 재밌었다. 각 아이템에서 이론에 입각한 주제로 설명하고 어떻게 코틀린의 방식으로 적용할 수 있을지 적어주었다. 
이전 장들처럼 단순 기술만 나열하지 않고 선 이유 설명 후 기술 설명으로 가니 설득도 되면서 저자의 의견에 더 귀를 기울이게 된다. 
이전까지는 각 장이 따로 노는 느낌이었다면, 이번 장은 배움의 연속이 느껴져 유익했다. 저번주에 잠시 얘기가 나왔던 복잡성과 연결된다. 
추상화는 복잡한 장치와 사용자 사이에서 더 단순한 형식으로 장치를 운용할 수 있게 도와주는 중요한 요소다. 
자바에서 인터페이스를 쓰는 이유를 전혀 몰랐는데, 이번엔 반 정도 이해가 갔다.

## Olive
### 느낀 점
이번 챕터는 읽기 전부터 많은 기대가 되었다. Charles께서 스터디 초반부터 계속해서 추상화의 중요성에 대해서 언급해주셨는데, 이번 챕터에서 추상화에 대해서 저자가
잘 설명하고 있다고 좋은 평을 주셨기 때문도 있고, 최근 회사 업무를 진행하면서 추상화를 어떻게 적용하면 좋을지 많은 고민을 하고 있었기 때문에 좋은 추상화 기법에 대한 나름대로의 호기심도 한 몫했다.

책에서는 전반적으로 추상화가 왜 중요한지, 우리 주변에서 쉽게 찾아볼 수 있는 추상화의 예시부터 시작해서, 단순히 추상화란 무엇인지가 아닌, 좋은 추상화를 위한 여러가지 고려할 요소들과 위험 요소들을 
단계적으로 빌드업하여 잘 설명해주고 있다. 그 중에서 가장 와닿았던 부분은, "추상화는 적절한 균형이 필요하다." 는 것인데, "균형"이라는 것이 여러가지 외부 환경적인 요소에의해 변할 수 있는 것이기 때문에
정량적인 지표로 표현될 수 없고, 수백 시간 이상의 경험이 필요하다는 것이다. 최근 회사 코드 내부에 적용된 추상화 개념들을 보면서 좋은 추상화에 대한 고민들을 계속해서하고 있는데, 단순히 잘했다 잘못했다로 귀결될 수 있는 요소들이 
아닌 것 같고, 나 조차도 경험적 요소가 부족하여 쉽게 판단하기 어려워서 공감이 많이 되었던 것 같다. 

끝으로 추상화는 언제나 어렵다. 좀 더 정확히는 "좋은 추상화"를 적용하는 것이 어려운 것 같다.  

# 토론 주제 
## 책에서 소개한 추상화의 정의는 적절하다고 생각하시나요?

> 복잡한 자료, 모듈, 시스템 등으로부터 핵심적인 개념 또는 기능을 간추려 내는 것

## 추상화는 언제 많이 사용하고 계신가요?

## 책에서 추상화의 균형을 맞추라고 하는데 추상화가 잘되었는지 어떻게 알 수 있을까요?

## 추상화 대상을 분리하는 기준이 있을까요?

## 안정적인 API의 기준은 무엇인가요? (안정적인 API를 설계하는 것이 가능할까요?)

## 추상화를 통한 상속과 컴포지션을 어떠한 기준을 가지고 선택해야 할까요?
