`spring-boot-starter-test`

### Test Scope Dependencies

The spring-boot-starter-test “Starter” (in the test scope) contains the following provided libraries:

- JUnit 5: The de-facto standard for unit testing Java applications.
- Spring Test & Spring Boot Test: Utilities and integration test support for Spring Boot applications.
- AssertJ: A fluent assertion library.
- Hamcrest: A library of matcher objects (also known as constraints or predicates).
- Mockito: A Java mocking framework.
- JSONassert: An assertion library for JSON.
- JsonPath: XPath for JSON.

We generally find these common libraries to be useful when writing tests. If these libraries do not suit your needs, you can add additional test dependencies of your own.

https://docs.spring.io/spring-boot/docs/current/reference/html/features.html#features.testing.test-scope-dependencies

<br/>

## 

<br/>

### @SpringBootTest 가 느린 이유!
 
애플리케이션을 로드할 때 Application Context에 빈을 등록하기 위해서 @Bean 으로 선언된 객체들을 찾는 등의 작업이 진행되기 때문에 시간이 오래 걸리게 된다. 

### 성능 개선 방법 

Context Caching

SpringBootTest는 context caching을 하므로 이를 이용해 Context 초기화가 한번만 이뤄지게하자.
  
  ```Once the TestContext framework loads an ApplicationContext (or WebApplicationContext) for a test, that context is cached and reused for all subsequent tests that declare the same unique context configuration within the same test suite. To understand how caching works, it is important to understand what is meant by “unique” and “test suite.”```
  
### 궁금한점 

-> 실제 객체가 필요한 상태 vs 테스트 더블을 사용해야할 상태인지 어떻게 알지?

https://meetup.nhncloud.com/posts/124
https://jiwondev.tistory.com/187
