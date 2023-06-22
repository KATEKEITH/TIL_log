# 문제 상황

프로젝트의 주문기능(https://github.com/f-lab-edu/goodchoice/pull/18/commits/b802375d5f913ffd63ece509ec65e90f3b40ccd5) 에 동시성 문제가 발생했다.

구매에 대한 트랜잭션에 대해서는 Redis를 사용하여 동시성 이슈를 처리하고, 데이터 유실 방지를 위해 트랜잭션 시점에 RDB에 데이터를 싱크하도록 하였다.
데이터 싱크를 위한 RDB 는 단일 엔티티로 단순 설계하여 재고량 증가 혹은 감소시점에 insert 쿼리만 발생하도록 하였다.

주문이 발생하면 Redis에 상품 재고(Stock)의 quantity를 업데이트 해서 실시간 재고를 관리하려고 했던게 문제였다.
간단한 자료형으로 데이터를 관리해야 하는데 RDB에 엔티티를 저장하는 것처럼 접근했던 것이었다.

<br/>

```
mport lombok.\*;
import org.springframework.data.redis.core.RedisHash;
import org.springframework.data.redis.core.TimeToLive;

import javax.persistence.Entity;
import javax.persistence.GeneratedValue;
import javax.persistence.GenerationType;
import javax.persistence.Id;
import java.io.Serializable;

@Getter
@NoArgsConstructor(access = AccessLevel.PROTECTED)
@AllArgsConstructor(access = AccessLevel.PRIVATE)
@Builder
@RedisHash(value = "stock")
public class Stock implements Serializable {

    @Id
    @GeneratedValue(strategy = GenerationType.IDENTITY)
    private Long id;

    private String itemToken;

    private Long quantity;

    @TimeToLive
    private long ttl;

    public Stock(String itemToken, Long quantity) {
        this.itemToken = itemToken;
        this.quantity = quantity;
    }

    public void decrease(Long quantity) {
        if (this.quantity - quantity < 0) {
            throw new RuntimeException("재고 부족");
        }

        this.quantity -= quantity;
    }

    public Long getQuantity() {
        return quantity;
    }

}
```

# 해결

Stock 엔티티(?)의 필드를 업데이트 할게 아니라 S0630000RU(상품번호):5000(상품명):stock:total G0BB0001JQ 와 같이 단순하게 셜계해서 재고 사용량을 업데이트 해야한다.
