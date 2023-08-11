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

다만 Reflection은 기본 생성자를 통해 객체를 생성하기 때문에 해당 클래스에 기본 생성자가 있어야 한다.
