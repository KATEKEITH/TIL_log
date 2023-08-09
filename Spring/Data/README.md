# Transaction

...

## Isolation

![image](https://github.com/KATEKEITH/TIL_log/assets/46472768/941f0a38-7739-43a3-ac6d-38b6c67e017e)


- SERIALIZABLE
- REPEATABLE READ
- READ COMMITTED
- READ UNCOMMITED


<br/>
<br/>


## Propagation

이미 트랜잭션이 진행중일 때 추가 트랜잭션 진행을 어떻게 할지 결정하는 것이다.

전파 속성에 따라 기존의 트랜잭션에 참여할 수도 있고, 별도의 트랜잭션으로 진행할 수도 있고, 에러를 발생시키는 등 여러 선택을 할 수 있다. <br/>

스프링에는 7가지 전파 속성이 존재하는데, REQUIRED와 REQUIRES_NEW를 바탕으로 어떻게 진행되는지 살펴보도록 하자.

![image](https://github.com/KATEKEITH/TIL_log/assets/46472768/1757d047-f9b2-4699-a3ec-393d88b1a6bf)

<br/>

### REQUIRED

![image](https://github.com/KATEKEITH/TIL_log/assets/46472768/b39d922b-807d-4515-8c0e-bf16e4d674f3)

내부 트랜잭션은 기존에 존재하는 외부 트랜잭션에 참여하게 된다.
여기서 참여한다는 것은 외부 트랜잭션을 그대로 이어간다는 뜻이며, 외부 트랜잭션의 범위가 내부까자 확장되는 것이다.
그러므로 내부 트랜잭션은 새로운 물리 트랜잭션을 사용하지 않는다.
하지만 트랜잭션 매니저에 의해 관리되는 논리 트랜잭션이 존재하므로 커밋은 내부 1회, 외부 1회해서 총 2회 실행된다.

의미: 트랜잭션이 필요함(없으면 새로 만듬)
기존 트랜잭션 없음: 새로운 트랜잭션을 생성함
기존 트랜잭션이 있음: 기존 트랜잭션에 참여함

REQUIRED는 디폴트 속성으로써 모든 트랜잭션 매니저가 지원하는 속성이다. 별도의 설정이 없다면 REQUIRED로 트랜잭션이 진행된다.

  <br/>

### REQUIRES_NEW

![image](https://github.com/KATEKEITH/TIL_log/assets/46472768/919eeb67-e48c-4aec-9b50-3382448d5e3b)

서로 다른 물리 트랜잭션을 별도로 가진다는 것은 각각의 디비 커넥션이 사용된다는 것이다.
즉, 1개의 HTTP 요청에 대해 2개의 커넥션이 사용되는 것이다.
내부 트랜잭션이 처리 중일때는 꺼내진 외부 트랜잭션이 대기하는데, 이는 데이터베이스 커넥션을 고갈시킬 수 있다.
그러므로 조심해서 사용해야 하며, 만약 REQURES_NEW 없이 해결 가능하다면 대안책(별도의 클래스를 두기 등)을 사용하는 것이 좋다.
