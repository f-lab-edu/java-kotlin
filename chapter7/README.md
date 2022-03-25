# 요약

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

# 토론 주제 

