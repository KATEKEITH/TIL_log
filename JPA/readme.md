# N+1

연관관계가 설정된 엔티티 사이에서 한 엔티티를 조회하였을 때,

조회된 엔티티의 개수(N 개)만큼 연관된 엔티티를 조회하기 위해 추가적인 쿼리가 발생하는 문제를 의미합니다.


<br/>

![image](https://github.com/KATEKEITH/daily_log/assets/46472768/7cb4f3fe-ab0c-41d8-83eb-98231798c977)

https://www.inflearn.com/questions/30446/%EC%A0%9C%EA%B0%80-%EC%9D%B4%ED%95%B4%ED%95%9C-%EA%B2%83%EC%9D%B4-%EC%A0%95%ED%99%95%ED%95%9C%EC%A7%80-%EA%B6%81%EA%B8%88%ED%95%A9%EB%8B%88%EB%8B%A4

<br/>

# How to solve this problem ?

``` 여러 번의 쿼리가 실행되지 않고 연관 관계가 있는 데이터까지 조인해서 데이터를 가져오면 된다. ```


1. Fetch join
2. EntityGraph


<br/>

Reference

https://velog.io/@hyunjong96/JPA-N1-%EB%AC%B8%EC%A0%9C-%EB%B0%8F-%ED%95%B4%EA%B2%B0%EB%B0%A9%EC%95%88

https://www.inflearn.com/questions/59632/fetch-join-%EA%B4%80%EB%A0%A8-%EC%A7%88%EB%AC%B8-%EB%93%9C%EB%A6%BD%EB%8B%88%EB%8B%A4

https://madplay.github.io/post/avoid-n+1-problem-in-jpa-using-querydsl-fetchjoin

https://thalals.tistory.com/295

https://devkuka.tistory.com/m/175

https://velog.io/@joonghyun/SpringBoot-JPA-JPA-Batch-Size%EC%97%90-%EB%8C%80%ED%95%9C-%EA%B3%A0%EC%B0%B0

https://velog.io/@antcode97/Fetch-Join%EC%9D%98-%ED%95%9C%EA%B3%84
