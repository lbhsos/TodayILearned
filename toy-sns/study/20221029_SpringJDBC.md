## 사전 필요 지식
### DataSource

- DB와의 연결을 위한 DB Server에 관한 정보(Property)를 설정한다.
    - ex. url, driver, username, password
- 정보를 기반으로 빈에 등록한다.
    - ex. BasicDataSource Bean
- 생성된 Bean을 Spring JDBC에 주입한다.

## JdbcTemplate
- DataSource를 설정한다.
- Spring JDBC 접근 방법 중 하나인 JdbcTemplate 객체를 생성하여 dataSource를 주입한다.
- CRUD API 를 제공한다.
- 개발자가 해야하는 작업
    1. SQL 문 작성
    2. 객체로 반환할 경우 mapRow()라는 interface method를 정의하여 결과를 처리하여야 한다.
    

## 기존 JAVA에서 DB 접근
1. 참조 블로그: [https://nankisu.tistory.com/10](https://nankisu.tistory.com/10)
2. JAVA의 JDBC를 사용한 DB 접근을 크게 5가지 동작으로 분류할 수 있다.
    1. DB에 대한 Connection을 DataSource에서 가져온다.
    2. SQL을 실행을 위한 Statement를 준비 한다.
    3. 실제 쿼리를 실행한다.
    4. RuleSet에서 데이터를 추출한다.
    5. 동작이 끝난 Connection, Statement, RuleSet을 close한다.

## NamedParameterJdbcTemplate
- 기존에 사용하던 JdbcTemplate에는 우리가 데이터를 넣을 부분에 `?` 를 이용하여 처리함
    - 가독성을 떨어뜨린다.
- ? 대신 :변수명 을 이용하여 처리함으로써 순서에 강제를 받지 않게된다.
    - Builder 패턴과 비슷한 느낌같다!
- 기존 JdbcTemplate 예시
```java
/* 이름이 Zara, 학번이 11인 학생을 삽입 */
String SQL = "insert into Student (name, age) values (?, ?)"; 
jdbcTemplateObject.update(SQL, new Object[]{"Zara", 11});
```
    
1. ParameterSource 를 통해 변수를 입력
```java
public int countOfActorsByFirstName(String firstName) {

    String sql = "select count(*) from T_ACTOR where first_name = :first_name";

    SqlParameterSource namedParameters = new MapSqlParameterSource("first_name", firstName);

    return this.namedParameterJdbcTemplate.queryForObject(sql, namedParameters, Integer.class);
}
```
    
2. Map을 통해 변수 입력

```java
public int countOfActorsByFirstName(String firstName) {

    String sql = "select count(*) from T_ACTOR where first_name = :first_name";

    Map<String, String> namedParameters = Collections.singletonMap("first_name", firstName);

    return this.namedParameterJdbcTemplate.queryForObject(sql, namedParameters,  Integer.class);
}
```

3. 객체 맵핑을 통한 변수 입력

```java
public class Actor {

    private Long id;
    private String firstName;
    private String lastName;

    public String getFirstName() {
        return this.firstName;
    }

    public String getLastName() {
        return this.lastName;
    }

    public Long getId() {
        return this.id;
    }
}
```

```java
public int countOfActors(Actor exampleActor) {

    String sql = "select count(*) from T_ACTOR where first_name = :firstName and last_name = :lastName";

    SqlParameterSource namedParameters = new BeanPropertySqlParameterSource(exampleActor);

    return this.namedParameterJdbcTemplate.queryForObject(sql, namedParameters, Integer.class);
}
```

## SimpleJdcbInsert
1. [스프링 JDBC 라이브러리](https://docs.spring.io/spring-framework/docs/current/javadoc-api/org/springframework/jdbc/core/simple/SimpleJdbcInsert.html)
2. 배경: JdbcTemplate으로 데이터를 삽입할 때 데이터의 pk를 얻고 싶을 때가 있는데, 기존 JdbcTemplate으로 구현할 수 있지만 코드의 가독성이 기하급수적으로 떨어져 스프링에서 가독성과 편의를 올려주는 클래스를 제공해준것

- JdbcTemplate으로 PK 구현 예시
    
```java
private final JdbcTemplate jdbcTemplate;

public StationDao(JdbcTemplate jdbcTemplate) {
    this.jdbcTemplate = jdbcTemplate;
}

public Station insert(final Station station) {
    try {
        String sql = "INSERT INTO station(name) VALUES(?)";

        KeyHolder keyHolder = new GeneratedKeyHolder();
        this.jdbcTemplate.update(connection -> {
            PreparedStatement ps = connection
                .prepareStatement(sql, new String[]{"id"});
            ps.setString(1, station.getName());
            return ps;
        }, keyHolder);

        return new Station(keyHolder.getKey().longValue(),
            station.getName());
    } catch (DuplicateKeyException e) {
        ...
    }
}
```
    
- SimpleJdbcInsert 예시

```java
private final JdbcTemplate jdbcTemplate;
private final SimpleJdbcInsert jdbcInsert;

public StationDao(JdbcTemplate jdbcTemplate, DataSource source) {
    this.jdbcTemplate = jdbcTemplate;
    this.jdbcInsert = new SimpleJdbcInsert(source) // 데이터소스로 DB에 접근해라.
        .withTableName("STATION")                  // 'STATION' 테이블에 삽입해라.
        .usingGeneratedKeyColumns("id");           // 'id' 컬럼의 값을 key로 반환해라.
}

public Station insert(Station station) {
    try {
        Map<String, String> params = new HashMap<>();
        params.put("name", station.getName());
        Long id = jdbcInsert.executeAndReturnKey(params).longValue(); // pk 값 얻기

        return new Station(id, station.getName());
    } catch (DuplicationKeyException e) {
        ...
    }
}
```
    
- 위 예시에서 primary key 값을 얻을 때 Map 자료구조를 사용하는데, 이를 대체하기 위해 SqlParameterSource 인터페이스를 구현한 다양한 객체를 제공하고 있다.
    - MapSqlParameterSource는 Map과 비슷하지만, addValue 메서드를 통해 체인으로 연결 가능
    - BeanPropertySqlParameterSource는 생성자, getter/setter를 가진 객체라면 사용 가능