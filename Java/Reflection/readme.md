

Batch 작업을 하기 위해서 오랜만에 JDBC를 사용할 일이 있었다.

분명 엔티티를 정의했는데 데이터가 null로 저장됬다???

```
@Getter
@NoArgsConstructor
@Entity
@ToString(exclude = {"team"})
```

Entity를 자세히 들여다 봤다. @Setter가 없다.

그렇다 JPA를 사용할땐 Entity에 @Setter를 붙여서 사용하지 않았다.

객체에 데이터를 넣기 위해서는 @Setter @Getter가 필요한게 맞고 접근 제어자에 따라 접근이 불가능한 것이 맞다.

하지만 JPA는 Reflection을 사용하기 때문에 이러한 과정이 필요하지 않고 private 메서드의 접근도 가능하다.

Reflection API를 통해 static 영역에 저장되어있는 클래스 정보에 접근이 가능하기 때문이다.

자바에서는 JVM이 실행되면 사용자가 작성한 자바 코드가 컴파일러를 거쳐 바이트 코드로 변환되어 static 영역에 저장된다. 

Reflection API는 이 정보를 활용한다. 그래서 클래스 이름만 알고 있다면 언제든 static 영역을 뒤져서 정보를 가져올 수 있는 것이다.

다만 Reflection은 기본 생성자를 통해 객체를 생성하기 때문에 해당 클래스에 기본 생성자가 있어야 한다.

```
Class carClass2 = Class.forName("Car");
```

또한 JPA에서 private 접근 제어자는 사용 불가능 한데, 이는 프록시와 관련이 있다.

지연로딩으로 인해 프록시 객체를 사용하는 경우 원본 엔티티를 상속한 프록시 객체를 생성하게 된다.

실제 사용 시점에 실제 엔티티 정보를 조회하여 프록시 엔티티가 원본 엔티티를 참조하도록 한다.

```
private -> default -> protected -> public
```

그러므로 기본 생성자에 private을 사용하게 된다면 상속받은 클래스(프록시 엔티티)에서 호출이 불가능하게 되고

public이나 protected 를 사용해야 한다는 오류가 발생하게 된다.

( protected는 동일 패키지의 클래스 또는 해당 클래스를 상속받은 다른 패키지의 클래스에서만 접근이 가능하다. )

 


