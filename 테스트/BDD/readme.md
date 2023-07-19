#

```

```

## Mockito

-> 원하는 동작을 미리 정하고 이를 기반으로 테스트

의존을 가지는 객체를 우리가 원하는 동작만 하도록 만든 것이 Mock 객체이다.
그리고 이런 Mock 객체를 직접 만들고 관리하기란 쉽지 않은데, Mockito는 이를 편하게 사용하도록 지원해주는 대표적인 테스트 프레임워크이다.

Spring에서 Mockito를 사용하기 위해서는 @ExtendWith(MockitoExtention.class)를 테스트 클래스 상단에 지정해주면 된다.
그러면 @Mock 어노테이션을 통해 간단하게 Mock 객체를 만들어 사용할 수 있다.

## BDDMockito

->

BDD 기본 패턴의 given에 해당하는 위치에 이전에 사용한 Mockito의 when() 메서드가 아닌 given() 메서드가 사용됨을 알 수 있다.

이 외로도 BDD 기본 패턴의 then에서 사용되는 Mockito에서 제공하는 verify()도 then().should()로 대체될 수 있다.
