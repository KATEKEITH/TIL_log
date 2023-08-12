![image](https://github.com/KATEKEITH/TIL_log/assets/46472768/26bfacbb-e6ea-4abd-82e1-0e718a86366c)


# 조인 테이블에 대한 조건은 WHERE보다 ON을 통해서 필터링하는 것이 성능을 최적화할 수 있는 방법이다.

ON을 사용할 경우 테이블들이 조인되기 전에 조건문을 수행한다.

반면에 WHERE 절은 테이블들이 조인된 후에 조건문이 수행되기에 더 많은 데이터를 필터링해야한다. 그러므로 성능을 저하시킬 수 있다.

## [INNER JOIN vs OUTER JOIN]

inner join은 존재하는 값에 대해서만 출력하기 때문에 조건의 위치나 테이블의 순서에 무관하게 같은 실행계획으로 같은 값이 출력됩니다. 

하지만 outer join을 사용하게되면 조건의 위치와 순서가 매우 중요해집니다.

( Inner Join의 경우 ON, Where 성능 차이는 크게 없으나, Outer Join의 데이터가 많으면 많을수록 큰 효과를 볼 수 있다. )


## INNER JOIN

### 1. INNER JOIN + ON 조건절 + ON 조건절

```
SELECT *
FROM a
INNER JOIN b
ON a.key = b.key
AND a.key2 = b.key2
```

### 2. EQUI JOIN + WHERE 조건절

```
SELECT *
FROM a AS a , b AS b
WHERE a.key = b.key
AND a.key2 = b.key2
```

### 3. INNER JOIN + ON 조건절 + WHERE 조건절

```
SELECT *
FROM a
INNER JOIN b
ON a.key = b.key
WHERE a.key2 = b.key2
```

## OUTER JOIN

outer join을 사용하는 의도는 특정 테이블의 모든 값이 포함된 결과를 보기 위해서 입니다.


