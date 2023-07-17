
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

## Slice Test

![image](https://github.com/KATEKEITH/TIL_log/assets/46472768/60f39144-0090-48b2-9dd6-e2783bf9dd7f)

```
Test slicing is about segmenting the ApplicationContext that is created for your test.
Typically, if you want to test a controller using MockMvc, surely you don’t want to bother with the data layer.
Instead you’d probably want to mock the service that your controller uses and validate that all the web-related interaction works as expected.
```


