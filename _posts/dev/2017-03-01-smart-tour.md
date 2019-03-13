---
layout: post
published: true
title: "[Dev] "
categories: dev
tags: dev 
---

# 1. 스마트투어 개발 가이드 

## 1.1 로컬 개발환경
> 개발환경은 All-In-One 구조로 다음과 같이 패키징 되어 있다. 

### 1.1.1 개발환경 설치 및 디렉토리 구조 
smart-tour.zip 파일을 다음의 경로에 압축 해제한다.

- Lombok
https://projectlombok.org/download

```
$ java -jar lombok.jar
```

* C:\smart-tour
  * apache-maven-3.3.9
  * eclipse 
  * java
    * jdk1.8.0_111
  * repository  
  : Maven 라이브러리 저장소
  * was
    * apache-tomcat-8.5.8
  * workspace
    * smart-tour

## 1.2 Project Structure
> smart-tour 프로젝트는 Maven Multi Project 로 구성되어 있다.

### 1.2.1 프로젝트 구조 
프로젝트는 모듈별로 다음과 같이 구성되어 있다.
* smart-tour
  * api
  * common
  * pom.xml

`smart-tour/pom.xml`
```xml
<modules>
    <module>api</module>
    <module>common</module>
</modules>
```

각 서브 어플리케이션(모듈)은 다음과 같이 `common` 모듈을 참조하도록 설정한다.

`pom.xml`
```xml
<dependency>
    <groupId>${project.groupId}</groupId>
    <artifactId>common</artifactId>
</dependency>
```

### 1.2.2 패키지 네이밍
각 서브 프로젝트별로 최상위 패키지 네이밍은 다음과 같다.  
com.smart-tour
* common  
* api  

업무별 비지니스 구현부분의 패키지 네이밍은 다음과 같이 구성한다.  
XXX 를 업무명이라고 가정할때, 레이어별로 패키지를 구분하여 구성한다.   
  * 업무패키지  
    * controller  
      * XXXController.java  
    * dao  
      * XXXDao.java  
    * doamin  
      * XXX.java  
    * repository  
      * XXXRepository.java  
    * service  
      * XXXService.java  
    * vo  
      * XXXVo.java  

## 1.3 Common 
> Smart-Tour 프로젝트의 공통 프레임워크를 위한 프로젝트

### 1.3.1 프레임워크 설정 정보
> 프레임워크 공통 설정 정보를 관리한다.

`src/main/resources/META-INF`
* datasource
* ehcache
* mybatis
* properties
* schedule
* spring
* system
* logback.xml

#### 1.3.1.1 DataSource 설정 

`datasource/datasource.properties`
```properties
# database configuration
smart-tour.jdbc.driverClass=org.hsqldb.jdbc.JDBCDriver

#DEV
smart-tour.jdbc.url=jdbc:hsqldb:mem:testdb
smart-tour.jdbc.username=sa
smart-tour.jdbc.password=
```

##### 트랜젹션 설정은 AOP에 의해서 동작하며 다음의 규칙을 따른다.

1. 트랜잭션은 `servicePointCut`에 지정된 서비스 클래스의 메서드만 대상이 된다.
1. find, select, get 로 시작하는 메서드는 `read-only` 속성을 따른다. 
1. 나머지 메서드는 런타임 예외발생 시 롤백되도록 설정한다.  
   단, Checked 예외인 경우는 롤백되지 않는다.

Note: `read-only` 속성의 경우는 사용하는 데이터베이스 및 드라이버에 따라서 기능을 지원하지 않을 수 있다. 

`datasource/datasource-transaction.xml`
```xml
<tx:advice id="txAdvice" transaction-manager="transactionManager">
    <tx:attributes>
        <tx:method name="find*" read-only="true" />
        <tx:method name="select*" read-only="true" />
        <tx:method name="get*" read-only="true" />
        <tx:method name="count*" read-only="true" />
        <tx:method name="list*" read-only="true" />
        <tx:method name="*" rollback-for="Throwable" />
    </tx:attributes>
</tx:advice>

<aop:config>
    <aop:pointcut id="servicePointCut" expression="execution(* com.smart-tour..service.*Service.*(..))" />
    <aop:advisor advice-ref="txAdvice" pointcut-ref="servicePointCut" />
</aop:config>
```

#### 1.3.1.2 Cache 설정 

`ehcache/ehcache.xml`
```xml
<cache name="service"
    maxElementsInMemory="10000"
    eternal="false"
    timeToIdleSeconds="300"
    timeToLiveSeconds="0"
    overflowToDisk="false"
    diskPersistent="false"
    diskExpiryThreadIntervalSeconds="120"
    memoryStoreEvictionPolicy="LRU">
</cache>
```

#### 1.3.1.3 mybatis 설정 
> 데이터베이스 프레임워크에 대한 설정 정보

* mapperLocations
  * SQL 정보를 저장하고 있는 Mapper 파일의 위치를 지정한다.
* basePackage
  * MyBatis Mapper 인터페이스로 사용하는 DAO 클래스를 스캔할 경로를 지정한다.

`mybatis/mybatis-context.xml`
```xml
<bean id="sqlSessionFactory" class="org.mybatis.spring.SqlSessionFactoryBean">
    <property name="dataSource" ref="dataSource"/>
    <property name="configLocation" value="classpath:META-INF/mybatis/mybatis-config.xml"/>
    <property name="mapperLocations" value="classpath*:META-INF/mybatis/mapper/**/*.xml" />
</bean> 

<bean class="org.mybatis.spring.mapper.MapperScannerConfigurer">
    <property name="basePackage" value="com.smart-tour" />
    <property name="annotationClass" value="org.springframework.stereotype.Repository"/>
</bean>
```

#### 1.3.1.4 프로퍼티 설정 
> 어플리케이션에서 사용하는 프로퍼티 설정 정보

* 환경별로 설정값이 달라지는 경우는 다음과 같이 프로퍼티 설정 파일의 확장자로 분리해서 관리한다.
  * local : application.properties
  * prd   : application.properties.prd

`properties/application.properties`
```
team.value=test
```

* 프로퍼티 설정파일을 분리하여 사용할 수도 있다.   
`system/system-context.xml`
```
<util:properties id="app" location="classpath:META-INF/properties/application.properties" />
<util:properties id="sys" location="classpath:META-INF/properties/system.properties" />
```

* 소스코드에서 사용법은 다음과 같다.  
`PropertyTest.java`
```java
public class PropertyTest {

    @Value("#{app['team.value']}")
    private String value;

    @Test
    public void value() {
        assertEquals("test", value);
    }
}
```

#### 1.3.1.5 스케쥴러 설정 
> 어플리케이션에서 스케쥴링에 의해서 실행되어야 하는 경우 다음과 같이 설정한다.

* 서버 인스턴스 별로 배치수행 여부를 지정하기 위해서 `@Profile` 기능을 사용한다.  
`TaskConfig.java`
```
@Configuration
@Profile("batch")
public class TaskConfig {

	@Bean
	public BatchScheduler batchScheduler() {
		return new BatchScheduler();
	}
}
```

* JVM 실행 arguments 부분에 다음과 같이 속성값을 지정하면 스케쥴러가 동작한다.
```
-Dspring.profiles.active=batch
```

* 수행되어야 하는 배치 서비스를 메서드로 호출하고 `@Scheduled` 어노테이션을 등록한다.
* 클론 표현식은 `"초 분 시 일 월 요일"` 형식으로 지정한다.   
`BatchScheduler.java`
```
public class BatchScheduler {

	@Resource
	ServiceInvoker serviceInvoker;

	@Scheduled(cron = "0 0 0 * * *")	// 초 분 시 일 월 요일
	public void invoke() {
	    serviceInvoker.invoke("TEAM", new Param());
	}
}
```

#### 1.3.1.6 로그 설정 
> 로그를 위한 설정을 관리한다.

* 로컬 개발환경에서는 디버깅이 필요할 경우 로그 레벨을 조정하여 필요한 로그 내역을 참조한다.
* 운영환경에서는 `INFO` 레벨 이상으로 로그 레벨을 설정한다.

`logback.xml`
```xml
<!-- 프레임워크 로그 레벨 조정 -->
<logger name="org.springframework" level="INFO" />
<logger name="org.mybatis.spring" level="INFO" />
<logger name="mapper" level="DEBUG" />
<logger name="org.apache.commons" level="WARN" />

<root level="DEBUG">
    <appender-ref ref="STDOUT" />
    <appender-ref ref="ROLLING" />
</root>
```

* 개발 및 운영환경에서는 파일로그를 출력하도록 설정하며 파일은 주기적으로 롤링하도록 설정한다. 

`logback.xml`
```xml
<appender name="ROLLING" class="ch.qos.logback.core.rolling.RollingFileAppender">
    <file>/log/smart-tour/api.log</file>
    <rollingPolicy class="ch.qos.logback.core.rolling.TimeBasedRollingPolicy">
        <!-- rollover daily -->
        <fileNamePattern>/log/smart-tour/api-%d{yyyy-MM-dd}.%i.log</fileNamePattern>
        <timeBasedFileNamingAndTriggeringPolicy class="ch.qos.logback.core.rolling.SizeAndTimeBasedFNATP">
            <maxFileSize>100MB</maxFileSize>
        </timeBasedFileNamingAndTriggeringPolicy>
    </rollingPolicy>
    <encoder>
        <pattern>%d{HH:mm:ss.SSS} [%thread] %-5level %logger{36} - %msg%n</pattern>
    </encoder>
</appender>
```

## 1.4 API Application 
> Client(Ionic App) 와 통신을 위해서 HTTP 프로토콜 기반으로 JSON 데이터를 송수신한다.

* REST 기반의 API 서버스를 위해서 RestController 를 구현한다. 
* 조회 기능은 MyBatis를 이용한 DAO 기반으로 구현한다.
* 등록, 수정, 삭제 기능은 Spring Data JPA 를 이용한 Repository 기반으로 구현한다.
* 개발의 용이성을 위해서 Service Interface 는 작성하지 않는다. 
* mapper 로 부터의 resultType 은 각 업무별 Vo 객체를 사용한다. 

### 1.4.1 서비스 호출 방식 

* URL  
  http://localhost:8080/api/todo

* 메서드   
  GET, POST, PUT, DELETE

* 메세지(요청/응답 데이터)
  ```json
  {"id":1,"title":"test","completed":false}
  ```

  Note: 모든 데이터는 키값이 반드시 존재해야 한다.

### 1.4.2 Sample Application 

#### Controller

`TodoController.java`
```java
@RestController
@RequestMapping("/todo")
public class TodoController {
    
    @Resource
    private TodoService todoService;

    @RequestMapping(method = RequestMethod.GET)
    public List<TodoVo> getTodos() {
        
        List<TodoVo> todoVoList = todoService.getTodos();

        return todoVoList;
    }

    @RequestMapping(value = "{id}", method = RequestMethod.GET)
    public Todo getTodo(@PathVariable Integer id) {

        Todo todo = todoService.getTodo(id);

        return todo;
    }

    @RequestMapping(method = RequestMethod.POST)
    @ResponseStatus(HttpStatus.CREATED)
    public Todo addTodo(@RequestBody Todo todo, BindingResult result) {

        todoService.addTodo(todo);
        
        return todo;
    }

    @RequestMapping(value = "{id}", method = RequestMethod.PUT)
    @ResponseStatus(HttpStatus.NO_CONTENT)
    public void updateTodo(@RequestBody Todo todo, @PathVariable Integer id) {

        todoService.updateTodo(todo);
    }

    @RequestMapping(value = "{id}", method = RequestMethod.DELETE)
    @ResponseStatus(HttpStatus.NO_CONTENT)
    public void deleteTodo(@PathVariable Integer id) {

        todoService.deleteTodo(id);
    }
}
```

#### Service

`TodoService.java`
```java
@Service
public class TodoService {

    @Resource
    private TodoDao todoDao;

    @Resource
    private TodoRepository todoRepository;

    public List<TodoVo> getTodos() {
        return todoDao.getTodos();
    }

    public Todo getTodo(int id) {
        return todoRepository.getOne(id);
    }

    public void addTodo(Todo todo) {
        todoRepository.save(todo);
    }

    public void updateTodo(Todo todo) {
        todoRepository.save(todo);
    }

    public void deleteTodo(int id) {
        todoRepository.delete(id);
    }
}
```

#### DAO

`TodoDao.java`
```java
@Repository
public interface TodoDao {

    public List<TodoVo> getTodos();

    public TodoVo getTodo(int id);

    public void addTodo(TodoVo teamVo);

    public void updateTodo(TodoVo teamVo);

    public void deleteTodo(int id);
}
```

### 1.4.3 단위 테스트 
> 단위 테스트 클래스는 단위 모듈을 테스트 하기 위해서 필요한 경우만 작성한다.

#### Service Test

`TeamServiceTest.java`
```java
@ContextConfiguration(locations = "classpath:META-INF/spring/root-context-test.xml")
@RunWith(SpringJUnit4ClassRunner.class)
public class TeamServiceTest {
    
    @Resource
    TeamService teamService;
    
    @Test
    public void getTeams() {
        List<TeamVo> list = teamService.getTeams(new Param());
        assertNotNull(list);
    }
}
```

#### Dao Test

`TeamDaoTest.java`
```java
@RunWith(SpringJUnit4ClassRunner.class)
@ContextConfiguration(locations = "classpath:META-INF/spring/root-context-test.xml")
public class TeamDaoTest {

    @Resource
    TeamDao teamDao;

    @Test
    public void getTeams() {
        List<TeamVo> list = teamDao.getTeams();
        assertNotNull(list);
    }
}
```

Note: 테스트 용이성을 위해서 ContextConfiguration 은 별도의 파일(root-context-test.xml)로 구성한다.

### 1.4.4 REST Test

#### API Server URL
https://smart-tour.herokuapp.com

#### API Test URL
https://smart-tour.herokuapp.com/swagger-ui.html

* swagger Api Documentation 화면으로 접속하여 다음과 같이 테스트를 수행한다.  
* 테스트 하려는 컨트롤러를 선택한다.
* 테스트 하려는 메서드를 선택한다.
* 다음과 같이 파라미터의 Value 부분에 요청 데이터를 입력한다.

Parameters
```
{
  "completed": true,
  "id": 0,
  "title": "테스트"
}
```

* `Try it out!` 버튼을 누르면 요청이 전송되고 응답이 돌아오면 결과값을 확인한다. 

Request URL
```
https://smart-tour.herokuapp.com/todos
```

Response Body
```
{
  "id": 1,
  "title": "테스트",
  "completed": true
}
```

Response Code
```
201
```
