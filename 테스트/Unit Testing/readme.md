## Slice Test

![image](https://github.com/KATEKEITH/TIL_log/assets/46472768/60f39144-0090-48b2-9dd6-e2783bf9dd7f)

```
Test slicing is about segmenting the ApplicationContext that is created for your test.
Typically, if you want to test a controller using MockMvc, surely you don’t want to bother with the data layer.
Instead you’d probably want to mock the service that your controller uses and validate that all the web-related interaction works as expected.
```
