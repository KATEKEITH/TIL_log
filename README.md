# TIL_log

기술과 지식을 나만의 언어로 정리하는 저장소입니다. 

<br>
<br>

## 자료 구조

### LinkedHashSet

![image](https://github.com/KATEKEITH/TIL_log/assets/46472768/17a3e266-37ed-490d-9049-8b3fe1819860)

```
package javaTest;

import java.util.Iterator;
import java.util.LinkedHashSet;
import java.util.Set;

public class LinkedHashSetTest {

	public static void main(String[] args) {
		  Set<String> set = new LinkedHashSet<String>();
	      
	      set.add("a");
	      set.add("z");
	      set.add("c");
	      set.add("b");
	      set.add("c"); //중복
	      set.add("p");
	      set.add("a"); //중복
	      set.add("d");
	      set.add("a"); //중복
	      
	      //Iterator 생성 방법 (*한번 생성 후 재사용 할경우 재생성 필수)
	      Iterator<String> iter = set.iterator();
	      
	      while(iter.hasNext()) {
	         System.out.println(iter.next());
	      }
          
          //Collectionx클래스의 sort를 쓰기위하여 Set의 객체들을 list에 담아 정렬.
          List<String> list = new LinkedList(set);
	      Collections.sort(list);
	}
}
```
![image](https://github.com/KATEKEITH/TIL_log/assets/46472768/3e220a7d-b0c8-43ec-846b-1d29dc9b191e)


<br>

## Spring

* Spring Core
  * IoC / DI

  * AOP - 예정
  * [스프링 입문을 위한 자바 객체 지향의 원리와 이해](./Spring/스프링%20입문을%20위한%20자바%20객체%20지향의%20원리와%20이해/README.md)
  * [빈 생명주기 및 콜백 메서드](./Spring/Core/bean%20lifecycle/bean%20lifecycle.md)
* Servlet

* Spring MVC

* Spring Boot

* Spring Cache

* Spring Data Redis
  * [Spring RedisTemplate Serializer 종류와 사용시 주의할 점](./Spring/Redis/redis%20serializer/serializer.md)
  * [Jedis vs Lettuce - 캐싱 예시](./Spring/Redis/jedis%20vs%20lettuce%20-%20캐싱/jedis%20vs%20lettuce%20-%20캐싱.md)
  * [Spring으로 Redis를 사용하기 전 보면 좋은 글 (Redis Client, RedisTemplate, RedisRepository)](./Spring/Redis/spring으로%20redis를%20사용하기%20전에%20보면%20좋은%20큰%20그림/spring으로%20redis를%20사용하기%20전에%20보면%20좋은%20큰%20그림.md)
  * [내장 Redis 서버 - Embedded Redis](./Spring/Redis/spring%20boot%20embedded%20redis%20server/spring%20boot%20embedded%20redis%20server.md)
* Spring Batch

* DB
  * [Spring Boot + JPA기반의 Replication 구현 (Multi DataSource)](./Spring/DB/Replication/Replication%20With%20JPA.md)
* Test
  * [Spring DB 테스트 격리 (DatabaseCleaner를 곁들인)](./Spring/Test/DB%20테스트%20격리/DB%20테스트%20격리.md)
* Event

* Spring Security

* Validation

* Logging

* 예외처리

* Rest Client

* MSA

* 커스텀

* 기타


<br>

## JPA
* [JPA 개념 정리 및 학습 테스트](https://github.com/binghe819/jpa-learning-sandbox)
* [cascade.REMOVE vs orphanremoval=true](./JPA/기타/cascade_remove_vs_orphanremoval/cascade_remove_vs_orphanremoval.md)
* N + 1
  * [N + 1 문제와 해결 방법](./JPA/N+1/N+1%20문제와%20해결%20방법.md)

<br>

## 빌드
* [Gradle이란 무엇인가?](./Build/Gradle%20기본/Gradle이란%20무엇인가.md)
* [Gradle 시작하기](./Build/Gradle%20기본/Gradle%20시작하기.md)
* 멀티 모듈
  * [멀티 모듈 적용하기 with Gradle, Spring](./Build/멀티%20모듈/멀티%20모듈%20적용%20with%20Gradle.md)

<br>

## 운영체제

 * Synchronous / Asynchronous
 * Blocking / Non-Blocking


<br>

## Infra & DevOps

* Docker
  
  ### 컨테이너 이미지 용량 줄이기
	![image](https://github.com/KATEKEITH/TIL_log/assets/46472768/4f6c4c48-67f3-4f47-b1e7-16fbccfa41ad)
	https://tech.cloudmt.co.kr/2022/11/08/container-imagesize-diet/


* AWS

* CI/CD


<br>

## 네트워크

### www.naver.com에 접속할 때 생기는 과정에 대해 설명해주세요.

![image](https://github.com/KATEKEITH/TIL_log/assets/46472768/85c2443a-19fe-4c45-aa56-785c2cc87242)

1. 사용자가 브라우저에 URL을 입력
2. 브라우저는 DNS를 통해 서버의 진짜 주소를 찾음
3. HTTP 프로토콜을 사용하여 HTTP 요청 메세지를 생성함
4. TCP/IP 연결을 통해 HTTP요청이 서버로 전송됨
5. 서버는 HTTP 프로토콜을 활용해 HTTP 응답 메세지를 생성함
6. TCP/IP 연결을 통해 요청한 컴퓨터로 전송
7. 도착한 HTTP 응답 메세지는 웹페이지 데이터로 변환되고, 웹 브라우저에 의해 출력되어 사용자가 볼 수 있게 됨

### TCP

TCP는 3 way-handshaking 과정을 통해 연결을 설정하고, 4 way-handshaking 과정을 통해 연결을 해제합니다.

3 way-handshake란 TCP 네트워크에서 통신 하는 장치가 서로 연결이 잘 되었는지 확인하는 방법입니다. 송신자와 수신자는 총 3번에 걸쳐 데이터를 주고 받으며 통신이 가능한 상태인지 확인합니다.
4 way-handshake란 TCP 네트워크에서 통신 하는 장치의 연결을 해제하는 방법입니다. 송신자와 수신자는 총 4번에 걸쳐 데이터를 주고 받으며 연결을 끊습니다.

![image](https://github.com/KATEKEITH/TIL_log/assets/46472768/21b0b43d-b209-4278-813c-b4521b5fa21e)

### OSI 7 layer와 각 계층에 대해 아는대로 설명해주세요.

![image](https://github.com/KATEKEITH/TIL_log/assets/46472768/aaf97bb5-1a7e-48aa-bbe3-78ef3f17ebb8)

7 계층(응용 계층) : 사용자에게 통신을 위한 서비스 제공. 인터페이스 역할
6 계층(표현 계층) : 데이터의 형식(Format)을 정의하는 계층 (코드 간의 번역을 담당)
5 계층(세션 계층) : 컴퓨터끼리 통신을 하기 위해 세션을 만드는 계층
4 계층(전송 계층) : 최종 수신 프로세스로 데이터의 전송을 담당하는 계층 (단위 :Segment) (ex. TCP, UDP)
3 계층(네트워크 계층) : 패킷을 목적지까지 가장 빠른 길로 전송하기 위한 계층 (단위 :Packet) (ex. Router)
2 계층(데이터링크 계층) : 데이터의 물리적인 전송과 에러 검출, 흐름 제어를 담당하는 계층 (단위 :frame) (ex. 이더넷)
1 계층(물리 계층) : 데이터를 전기 신호로 바꾸어주는 계층 (단위 :bit) (장비: 케이블,리피터,허브)


### RESTful API란 무엇인가요?

RESTful API는 두 컴퓨터 시스템이 인터넷을 통해 정보를 안전하게 교환하기 위해 사용하는 인터페이스입니다.
대부분의 비즈니스 애플리케이션은 다양한 태스크를 수행하기 위해 다른 내부 애플리케이션 및 서드 파티 애플리케이션과 통신해야 합니다.
예를 들어 월간 급여 명세서를 생성하려면 인보이스 발행을 자동화하고 내부의 근무 시간 기록 애플리케이션과 통신하기 위해 내부 계정 시스템이 데이터를 고객의 뱅킹 시스템과 공유해야 합니다. 
RESTful API는 안전하고 신뢰할 수 있으며 효율적인 소프트웨어 통신 표준을 따르므로 이러한 정보 교환을 지원합니다.



### HTTP의 GET과 POST 비교

GET
우선 GET 방식은 요청하는 데이터가 HTTP Request Message의 Header 부분에 url 이 담겨서 전송된다. 때문에 url 상에 ? 뒤에 데이터가 붙어 request 를 보내게 되는 것이다. 이러한 방식은 url 이라는 공간에 담겨가기 때문에 전송할 수 있는 데이터의 크기가 제한적이다. 또 보안이 필요한 데이터에 대해서는 데이터가 그대로 url 에 노출되므로 GET방식은 적절하지 않다. (ex. password)

POST
POST 방식의 request 는 HTTP Request Message의 Body 부분에 데이터가 담겨서 전송된다. 때문에 바이너리 데이터를 요청하는 경우 POST 방식으로 보내야 하는 것처럼 데이터 크기가 GET 방식보다 크고 보안면에서 낫다.(하지만 보안적인 측면에서는 암호화를 하지 않는 이상 고만고만하다.)

그렇다면 이러한 특성을 이해한 뒤에는 어디에 적용되는지를 알아봐야 그 차이를 극명하게 이해할 수 있다. 우선 GET 은 가져오는 것이다. 서버에서 어떤 데이터를 가져와서 보여준다거나 하는 용도이지 서버의 값이나 상태 등을 변경하지 않는다. SELECT 적인 성향을 갖고 있다고 볼 수 있는 것이다. 반면에 POST 는 서버의 값이나 상태를 변경하기 위해서 또는 추가하기 위해서 사용된다.

부수적인 차이점을 좀 더 살펴보자면 GET 방식의 요청은 브라우저에서 Caching 할 수 있다. 때문에 POST 방식으로 요청해야 할 것을 보내는 데이터의 크기가 작고 보안적인 문제가 없다는 이유로 GET 방식으로 요청한다면 기존에 caching 되었던 데이터가 응답될 가능성이 존재한다. 때문에 목적에 맞는 기술을 사용해야 하는 것이다.


### TCP
![image](https://github.com/KATEKEITH/TIL_log/assets/46472768/6666c2a3-f98d-456d-9aea-6b6ec9ffaf63)

대부분의 인터넷 응용 분야들은 신뢰성 과 순차적인 전달 을 필요로 한다. UDP 로는 이를 만족시킬 수 없으므로 다른 프로토콜이 필요하여 탄생한 것이 TCP이다. TCP(Transmission Control Protocol, 전송제어 프로토콜)는 신뢰성이 없는 인터넷을 통해 종단간에 신뢰성 있는 바이트 스트림을 전송 하도록 특별히 설계되었다. TCP 서비스는 송신자와 수신자 모두가 소켓이라고 부르는 종단점을 생성함으로써 이루어진다. TCP 에서 연결 설정(connection establishment)는 3-way handshake를 통해 행해진다.

모든 TCP 연결은 전이중(full-duplex), 점대점(point to point)방식이다. 전이중이란 전송이 양방향으로 동시에 일어날 수 있음을 의미하며 점대점이란 각 연결이 정확히 2 개의 종단점을 가지고 있음을 의미한다. TCP 는 멀티캐스팅이나 브로드캐스팅을 지원하지 않는다.

https://valueelectronic.tistory.com/102

<br>

## 데이터베이스

* 데이터 모델링

* 관계형 데이터베이스
  
* SQL
  
  * 인덱스틑 타는지 확인하는 방법( https://github.com/gwonsungjun/wiki/blob/master/RDB/MySQL/mysql-explain.md )

  * DB 인덱스를 타지 못하는 경우( https://helloworld92.tistory.com/18 )
    
    * OR 조건 일 경우 
    ```select * from table where name = 'word' or idx = 5```
  
    OR 조건의 특징은 'A OR B'일 경우 A가 True이면 B를 수행하지 않고 A가 False일 경우 B를 수행한다.
    name과 idx가 둘다 인덱스가 걸려있는 경우라해도, DBMS가 최적의 OR 조건을 뽑기 힘들어, FULL SCAN 하는 경우가 많다.
  
  * 책
    * [친절한 SQL 튜닝](./SQL/test)

* [h2](./DB/RDB/h2/h2.md)

* MySQL

* Redis
 
* ElasticSearch

* MongoDB

* 기타

<br>

## JAVA
* JAVA Core

* 로깅

* Test

* 기타

* Java Convention


<br>

## OOP 및 아키텍처

객체 지향 프로그래밍은 컴퓨터 프로그램을 명령어의 목록으로 보는 시각에서 벗어나 여러 개의 독립된 단위, 즉 "객체"들의 모임으로 파악하고자 하는 것이다. 
각각의 객체는 메시지를 주고받고, 데이터를 처리할 수 있다.

객체 지향 프로그래밍은 프로그램을 유연하고 변경이 쉽게 만들기 때문에 대규모 소프트웨어 개발에 많이 사용된다.

* 책
  * [객체 지향 프로그래밍 입문](./OOP/%EA%B0%9D%EC%B2%B4%20%EC%A7%80%ED%96%A5%20%ED%94%84%EB%A1%9C%EA%B7%B8%EB%9E%98%EB%B0%8D%20%EC%9E%85%EB%AC%B8)

* SOLID
  * [SRP](./OOP&설계/SOLID/SRP.md)
  * [OCP](./OOP&설계/SOLID/OCP.md)
  * [LSP](./OOP&설계/SOLID/LSP.md)
  * [ISP](./OOP&설계/SOLID/ISP.md)
  * [DIP](./OOP&설계/SOLID/DIP.md)
* 디자인 패턴
  * [전략 패턴](./OOP&설계/%EB%94%94%EC%9E%90%EC%9D%B8%ED%8C%A8%ED%84%B4/Strategy%20Pattern.md)
  * [템플릿 메서드 패턴](./OOP&설계/%EB%94%94%EC%9E%90%EC%9D%B8%ED%8C%A8%ED%84%B4/Template%20Method%20Pattern.md)
  * [상태 패턴](./OOP&설계/%EB%94%94%EC%9E%90%EC%9D%B8%ED%8C%A8%ED%84%B4/State%20Pattern.md)
  * [프론트 컨트롤 패턴](./OOP&설계/%EB%94%94%EC%9E%90%EC%9D%B8%ED%8C%A8%ED%84%B4/Front%20Controller%20Pattern.md)
  * [데코레이터 패턴](./OOP&설계/%EB%94%94%EC%9E%90%EC%9D%B8%ED%8C%A8%ED%84%B4/Decorator%20Pattern.md)
  * [프록시 패턴와 데코레이터 패턴](./OOP&설계/%EB%94%94%EC%9E%90%EC%9D%B8%ED%8C%A8%ED%84%B4/../디자인패턴/Proxy%20Pattern와%20Decorator%20pattern.md)
  * [다이내믹 프록시](./OOP&설계/디자인패턴/Dynamic%20Proxy.md)
* 기타

<br>

