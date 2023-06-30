# N+1

<br/>

JPA에서 제공하는 findById()와 같은 메소드는 EntityManager에서 id을 가지고 객체를 조회하는 JPQL을 생성한다. 
이때 연관관계 객체가 즉시로딩으로 되어 있을 때 Join절을 이용해 1개의 쿼리를 생성하여 연관관계 객체를 가져오게된다.

하지만 문제는 JPQL을 만들때 발생한다. 
findAll()과 같은 메소드를 사용할 때 JPA는 전체 Owner를 조회하는 SELECT * FROM OWNER 쿼리를 생성하게 될것이고 연관관계를 가져올수 없게 된다. 
그렇기 때문에 연관관계를 가져오기 위한 또 다른 SELECT 쿼리를 생성하게 되고 OWNER의 개수만큼 연관관계를 가져와야하기 때문에 OWNER 개수만큼 SELECT 쿼리가 생성된다.
즉, Owner를 가져오기 위한 SELECT쿼리(1)과 Owner만큼의 연관관계를 조회하기 위한 SELECT쿼리(N)이 데이터베이스에 요청되게 된다.

이것이 N+1문제이다.

마찬가지로 findByName()과 같은 쿼리메소드는 Join문을 지원해주지 않는다.

<br/>


Reference

https://velog.io/@hyunjong96/JPA-N1-%EB%AC%B8%EC%A0%9C-%EB%B0%8F-%ED%95%B4%EA%B2%B0%EB%B0%A9%EC%95%88
