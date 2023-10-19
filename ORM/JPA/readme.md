
# JPA ( Java Persistent API )와 ORM ( Object Relational Mapping )

JPA란 자바 ORM 기술에 대한 API 표준 명세를 의미합니다.

JPA는 ORM을 사용하기 위한 인터페이스를 모아둔 것이며, 

JPA를 사용하기 위해서는 JPA를 구현한 Hibernate, EclipseLink, DataNucleus 같은 ORM 프레임워크를 사용해야 합니다.

![image](https://github.com/KATEKEITH/TIL_log/assets/46472768/9b688bd8-d743-49db-8e59-66a3150596ad)


보통 하이버네이트는 메모리에 영속 가능한 상태를 유지한다. 이 상태를 DB 에 동기화(적용)하는 것을 "flushing" 이라고 한다.

우리가 save() 메소드를 수행할 때, 처리되는 데이터는 flush()  또는 commit() 메소드가 실행되기 전까지 DB로 flush 되지 않는다.

즉, 우리가 하이버네이트로 구현한 JPA 를 사용할 때, 특정 구현체? 객체? 가 flush() 또는 commit() 동작을 관리한다.

한 가지 알아야 할 점은, commit 을 수행하지 않고 직접 flush를 수행한다면 트랜잭션 외부에서 알 수가 없다.

<br/>

![image](https://github.com/KATEKEITH/TIL_log/assets/46472768/efbb9101-a5dc-4315-94bc-ebb53107d462)

```
- save() 메소드와는 다르게 saveAndFlush() 메소드는 실행중(트랜잭션)에 즉시 data를 flush 한다.

- saveAndFlush() 메소드는 Spring Data JPA 에서 정의한 JpaRepository 인터페이스의 메소드이다.
```
