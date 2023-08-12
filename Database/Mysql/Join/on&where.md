# 조인 테이블에 대한 조건은 WHERE보다 ON을 통해서 필터링하는 것이 성능을 최적화할 수 있는 방법이다.

ON을 사용할 경우 테이블들이 조인되기 전에 조건문을 수행한다.
반면에 WHERE 절은 테이블들이 조인된 후에 조건문이 수행되기에 더 많은 데이터를 필터링해야한다. 그러므로 성능을 저하시킬 수 있다.
Inner Join의 경우 ON, Where 성능 차이는 크게 없으나, Outer Join의 데이터가 많으면 많을수록 큰 효과를 볼 수 있다.

## [ON vs WHERE]

ON : JOIN 을 하기 전 필터링을 한다 ( = ON 조건으로 필터링이 된 레코들간 JOIN이 이뤄진다)

WHERE : JOIN 을 한 후 필터링을 한다 ( = JOIN을 한 결과에서 WHERE 조건절로 필터링이 이뤄진다)

### INNER JOIN + ON 조건절 + ON 조건절

```
SELECT *
FROM a
INNER JOIN b
ON a.key = b.key
AND a.key2 = b.key2
```

### EQUI JOIN + WHERE 조건절

```
SELECT *
FROM a AS a , b AS b
WHERE a.key = b.key
AND a.key2 = b.key2
```

### INNER JOIN + ON 조건절 + WHERE 조건절

```
SELECT *
FROM a
INNER JOIN b
ON a.key = b.key
WHERE a.key2 = b.key2
```
