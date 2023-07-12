# DI의 3가지 방식

- Field injection

Field Injection은 프로젝트를 하면서 가장 자주 접하게 되는 주입 방식입니다.
setter기반과 마찬가지로 빈 생성이 완료된 이후 주입되며, 마찬가지로 final로 선언할 수 없습니다.
하지만 앞선 다른 방식들과 다르게 간단하게 필드에 @Autowired 같은 애너테이션만 달아주기 때문에
매우 간결해 보이며 유지보수에 편해 보입니다.

- Setter injection

Setter 기반 DI는 다음과 같이 setter메서드에 사용합니다.
여기서 @Autowired 애너테이션은 생략될 수 없으며,
빈 생성과 동시에 주입되지 않고, 빈 생성이 끝난 후 setter을 호출하여 주입합니다.
그렇기 때문에 final을 사용할 경우 컴파일 에러가 발생합니다.

- Constructor injection

빈 생성시점에 주입됨으로써,주입받는 필드를 final로 상수 선언이 가능하다는 점이 장점이다.
이 점은 필수적인 디팬던시를 관리할 때 편리합니다. (Required Dependencies)

# Field Injection이 왜 나쁜가

## Single Responsibility Principle

## DI 컨테이너에 강한 결합 발생

## 주입된 객체는 Immutable한 상태를 만들 수 없다.

오직 Constructor Injection 만이 final 선언이 가능합니다.
나머지 방법은 주입되는 필드에 대해 mutable한 상태를 만들기 때문에
가급적이면 생성자 주입을 적용하는게 좋습니다.
