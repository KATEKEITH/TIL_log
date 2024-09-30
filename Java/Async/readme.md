


<br/>
<br/>
<br/>

![image](https://github.com/user-attachments/assets/9f0acd8c-b21f-4cc6-8ef6-4267772e22fb)

<br/>

|제목|내용|설명|
|------|---|---|
|Spring WebFlux|리액티브 방식으로 HTTP 요청을 처리하는 프레임워크입니다. 이는 비동기 처리 및 논블로킹 I/O를 지원하여 더 많은 동시 요청을 처리할 수 있게 해줍니다.|테스트3|
|테스트1|테스트2|테스트3|
|테스트1|테스트2|테스트3|

<br/>

### Socket Channel
요청은 소켓 채널을 통해 애플리케이션 내부로 전달됩니다. 이때 비동기적인 방식으로 요청이 처리될 수 있습니다.

<br/>

### Servlet API

Servlet API는 자바 기반 웹 애플리케이션에서 HTTP 요청과 응답을 처리하기 위한 규약(인터페이스와 클래스)의 모음입니다.
**서블릿(Servlet)**이 HTTP 요청을 처리할 수 있도록 도와주는 표준 인터페이스로, 자바에서 웹 서버나 애플리케이션 서버와 상호 작용할 때 사용됩니다.
주로 Tomcat, Jetty, Undertow 같은 서블릿 컨테이너에서 동작하며, 이 컨테이너들은 Servlet API를 사용해 웹 애플리케이션의 HTTP 요청과 응답을 관리합니다.


<br/>


## 자바에서 비동기로 구현하면 trace_id가 유실 되는 이유

```

```

<br/>
<br/>
<br/>

## 로깅 - 비동기 태스크 수행 중 오류가 나면 요청 URL 이나 사용자정보 등 많은 정보들이 나타나지 않는다?

```
MDC 는 기본적으로 ThreadLocal을 만들어서 정보를 저장한다!
```

스프링에서 Web Request가 오게 되면 하나의 쓰레드를 할당해서 해당 작업을 처리하게 되는데, 이때 Thread 에 대한 정보를 ThreadLocal 에 저장하게 되면 해당 작업이 끝날 때 까지 모든 상황에서 context 를 유지하고 저장하고 찾아볼 수 있어서 편하다. MDCAdapter 가 이런 방식을 활용해서 구현이 되어있기에 MDC를 많이 사용했다.

### 하지만, 비동기 처리를 위해 TaskExecutor 를 활용하기 시작하면 해당 executor 는 새로운 Thread 를 생성하게 되는데 이 쓰레드에는 기존 쓰레드의 context 가 넘어가지 않고 새로 만들어지기 때문에 저렇게 다 빈값으로 나오게 된다.

다시 말해 비동기 처리시 logging 정보를 지금처럼 ThreadLocal 사용하게 되면 스레드에 저장된 정보가 새로운 비동기 쓰레드에 전달 안됨 → 스레드 context 활용하는 MDCUtil 을 이용해 처리하는 모든 로깅이나 로직이 먹통이 된다.

### TaskDecorator

Spring 4.3 이상부터 제공되는 TaskDecorator 를 이용해서 비동기처리하는 taskExecutor 생성시 커스터마이징이 가능하다는 것을 찾게 되었습니다.

기존 스레드의 MDC 전체값을 카피해서 넣어 버리는 형태인데 당연히 기존 스레드와 분리 되어 있어서 값만 일치 할뿐 서로 연결되지 않으니 side effect 도 없어보였습니다.

```
public class ClonedTaskDecorator implements TaskDecorator {

		@Override
		public Runnable decorate(Runnable task) {

			Map<String, String> callerThreadContext = MDC.getCopyOfContextMap();
			return () -> {
				MDC.setContextMap(callerThreadContext);
				task.run();
			};
		}
}
```

그리고 아래처럼 설정하면서 setTaskDecorator 를 이용해 위에 생성된 것을 세팅합니다.

```
@Configuration
@EnableAsync
public class AsyncConfig {

	@Bean
	public TaskExecutor taskExecutor() {
		ThreadPoolTaskExecutor taskExecutor = new ThreadPoolTaskExecutor();

		// 아시겠지만.. corePool 이 기본 스레드 풀 개수
		// maxPool 이 최대 개수
    // queueCapacity 가 맥스이상의 업무가 몰려오면 큐 개수만큼은 저장해둘 수 있다는 뜻. 단, 그 이상이 들어오면 탈락시켜버린다.
		taskExecutor.setCorePoolSize(20);
		taskExecutor.setMaxPoolSize(50);
		taskExecutor.setQueueCapacity(200);
		taskExecutor.setMaxPoolSize(50);
		// 내가 만든 데코레이터 설정
		taskExecutor.setTaskDecorator(new ClonedTaskDecorator());
		taskExecutor.setThreadNamePrefix("async-task-");
		taskExecutor.setThreadGroupName("async-group");

		return taskExecutor;
	}

}
```

https://blog.gangnamunni.com/post/mdc-context-task-decorator/
https://steady-coding.tistory.com/611
https://jsonobject.tistory.com/468
