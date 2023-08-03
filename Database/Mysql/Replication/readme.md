

# Replication 동작 원리

![image](https://github.com/KATEKEITH/daily_log/assets/46472768/3533d203-ca8b-4f09-885c-77545483bc6b)

1. Client가 쓰기 쿼리 작업을 요청합니다. 쓰기 쿼리요청은 Master DB가 받습니다.
2. Master는 변경사항을 Binary log 파일에 기록합니다. 이후 DB에 반영(commit)합니다.
3. Slave는 현재까지 기록한 이벤트 정보 (GTID=2)를 가지고 다음 이벤트 정보를 Master에게 요청합니다.
4. Master는 Binary log 파일에서 최신 이벤트 정보(GTID=3)를 읽어
5. Slave에게 전송합니다.
6. Slave는 Master에게 받은 이벤트 정보(GTID=3)를 Relay log 파일에 기록합니다.
7. Slave는 최종 변경사항을 DB에 반영(commit)합니다.

 4,5 과정에서는 Master 쓰레드, 3, 6 과정에서는 Slave I/O 쓰레드, 7 과정에서는 Slave SQL 쓰레드가 동작합니다. 

( https://it-sunny-333.tistory.com/148 )

<br/>
<br/>

# Master/Slave DataSource 동적 라우팅 설정


## AbstractRoutingDataSource 
```
public class DynamicRoutingDataSource extends AbstractRoutingDataSource {

    @Override
    protected Object determineCurrentLookupKey() {
        return isCurrentTransactionReadOnly() ? SLAVE : MASTER;
    }
}
```

AbstractRoutingDataSource는 다중 DataSource를 묶고 키를 통해 상황에 따라 동적으로 라우팅할 수 있도록 도와준다.
determineCurrentLookupKey를 이용해 라우팅할 DataSource의 키를 선택하는데 isCurrentTransactionReadOnly() 메소드를 통해 트랜잭션의 readOnly 여부를 알아내서 readOnly라면 slave DB로, readOnly가 아니라면 master DB로 라우팅되도록 상수 키를 반환한다.

<br/>

## DataSource

```
public class RoutingDataSourceConfig {
  
    @ConfigurationProperties(prefix = "spring.datasource.hikari.master")
    @Bean
    public DataSource masterDataSource() {
        return DataSourceBuilder.create().type(HikariDataSource.class).build();
    }

    @ConfigurationProperties(prefix = "spring.datasource.hikari.slave")
    @Bean
    public DataSource slaveDataSource() {
        return DataSourceBuilder.create().type(HikariDataSource.class).build();
    }

}
```
master와 slave DataSource는 ConfigurationProperties를 통해 설정값을 바인딩하여 간단하게 만들 수 있다. 그리고 아까 만들었던 DynamicRoutingDataSource에 master와 slave DataSource를 타겟으로 추가해준다.

<br/>

```
public class RoutingDataSourceConfig {
  
    @DependsOn({"masterDataSource", "slaveDataSource"})
    @Bean
    public DataSource routingDataSource(
        @Qualifier("masterDataSource") DataSource master,
        @Qualifier("slaveDataSource") DataSource slave) {
        DynamicRoutingDataSource routingDataSource = new DynamicRoutingDataSource();

        Map<Object, Object> dataSourceMap = new HashMap<>();

        dataSourceMap.put(MASTER, master);
        dataSourceMap.put(SLAVE, slave);

        routingDataSource.setTargetDataSources(dataSourceMap);
        routingDataSource.setDefaultTargetDataSource(master);

        return routingDataSource;
    }

    @DependsOn({"routingDataSource"})
    @Bean
    public DataSource dataSource(DataSource routingDataSource) {
        return new LazyConnectionDataSourceProxy(routingDataSource);
    }

}
```

여기서 중요한 것은 spring에서는 원래 Transaction 동기화 이전에 DataSource에서 Connection을 획득한다. 하지만 우리는 Transaction 동기화 이후 실제 쿼리 호출 시 DataSource를 정하고 Connection을 획득해야만 하기 때문에 문제가 발생한다.  

따라서 LazyConnectionDataSourceProxy를 통해 routingDataSource를 감싸주어서 Tracnsaction 동기화 이전에는 Connection Proxy 객체를 획득하고 이 후 쿼리가 호출될 때에 DataSource를 정하고 Connection을 획득할 수 있도록 늦춰주었다. 따라서 LazyConnectionDataSourceProxy를 통해 routingDataSource를 감싸주어서 Tracnsaction 동기화 이전에는 Connection Proxy 객체를 획득하고 이 후 쿼리가 호출될 때에 DataSource를 정하고 Connection을 획득할 수 있도록 늦춰주었다.

또한 순환 참조가 발생할 수 있기 때문에 DependsOn 어노테이션을 이용해서 Bean들간의 의존 관계를 명시해주었다.

## dependsOn
@DependsOn({"testA","testB"}) 와 같은 형태로 자신보다 먼저 초기화되어야 할 POJO 를 여러개 명시할 수 있습니다.

<br/>

## EntityManagerFactory, TransactionManager
```
    @Primary
    @Bean
    public LocalContainerEntityManagerFactoryBean entityManagerFactory(DataSource dataSource) {
        LocalContainerEntityManagerFactoryBean em = new LocalContainerEntityManagerFactoryBean();
        em.setJpaVendorAdapter(new HibernateJpaVendorAdapter());
        em.setDataSource(dataSource);
        em.setPackagesToScan("\");

        Map<String, Object> properties = new HashMap<>();
        properties.put("hibernate.physical_naming_strategy",
            SpringPhysicalNamingStrategy.class.getName());
        properties.put("hibernate.implicit_naming_strategy",
            SpringImplicitNamingStrategy.class.getName());
        properties.put("hibernate.hbm2ddl.auto", env.getProperty("spring.jpa.hibernate.ddl-auto"));
        em.setJpaPropertyMap(properties);

        return em;
    }

    @Primary
    @Bean
    public PlatformTransactionManager transactionManager(EntityManagerFactory entityManagerFactory) {
        JpaTransactionManager transactionManager = new JpaTransactionManager();
        transactionManager.setEntityManagerFactory(entityManagerFactory);

        return transactionManager;
    }
 ```
...

( https://kerobero.tistory.com/39 )

