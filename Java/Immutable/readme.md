## 변경 가능성을 최소화하라

불변 클래스란 간단히 말해 그 인스턴스의 내부 값을 수정할 수 없는 클래스다.
불변 객체는 단순하다.
불변 객체는 생성된 시점의 상태를 파괴될 때까지 그대로 간직한다.
불변 객체는 근본적으로 스레드 안전하여 따로 동기화할 필요가 없다.

## Immutability를 보장해야하는 경우

다음과 같이 UserRequest의 정보를 토대로 사용자에게 콜백을 보내는 기능이 있었다.
sessionKey는 변경이 되면 안되는 값이라 이론적으로는 고객이 뭔가 착각했음을 알고 있었지만 확인이 필요했다. 왜냐하면 위의 UserRequest에는 sessionKey에 대한 Setter가 구현되어 있었으므로 변경 가능성이 있었기 때문이다. 만약 내가 짠 코드라면 변경 메소드를 호출하지 않았음을 조금 더 쉽게 파악할 수 있었겠지만 내가 짠 코드가 아니였고, 수정자 메소드가 있으므로 변경 여뷰를 파악해야 했었다.

```
@Getter
@Setter
public class UserRequest {

    private String sessionKey;

}

@RequiredArgsConstructor
@Service
public class UserService {

    public void sendCallBack(User user, UserRequest userRequest) {
        validateConfigInfo(user, userRequest);
        updateLastUserRequest(user, userRequest);

        ... /// 300 라인

        send(user, userRequest);
    }

}
```

https://mangkyu.tistory.com/131

## Immutable Object

https://devoong2.tistory.com/entry/Java-%EB%B6%88%EB%B3%80-%EA%B0%9D%EC%B2%B4Immutable-Object-%EC%97%90-%EB%8C%80%ED%95%B4-%EC%95%8C%EC%95%84%EB%B3%B4%EC%9E%90
