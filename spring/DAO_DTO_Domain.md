# DAO / DTO / Domain

## Table of contents

[1. DAO](#1-dao--data-access-object)<br>
[2. DTO](#2-dto-data-transfer-object)<br>
[3. Domain](#3-domain---entity)<br>

---

## 1. DAO ( Data Access Object )

- **repository package**
  - 실제로 DB에 접근하여 Data를 CRUD하는 객체.
  - Service와 DB를 연결 해주는 역할.
  - 인터페이스와 이에 대한 구현체를 만들어서 구현체에 CRUD 관련 기능을 구현하고, 이를 DI 해주는 방식으로 사용.

  - 인터페이스
  ```java
  public interface MemberRepository {

  	Member save(Member member);
  	Optional<Member> findById(Long id);
  	Optional<Member> findByName(String name);
  	List<Member> findAll();
  }
  ```
  - 구현체
  ```java
  public class JpaMemberRepository implements MemberRepository {

  	...

  	@Override
  	public Member save(Member member) {
  		...
  	}

  	@Override
  	public Optional<Member> findById(Long id) {
  		...
  	}

  	@Override
  	public Optional<Member> findByNames(String name) {
  		...
  	}

  	@Override
  	public List<Member> findAll() {
  		...
  	}

  	...
  }
  ```
  - DI
  ```java
  @Configuration
  public class SpringConfig {
  	...

  	@Bean
  	public MemberRepository memberRepository(){
  		return new JpaMemberRepository(em);
  	}
  	...
  }
  ```

---

## 2. DTO (Data Transfer Object)

- **dto package**
  - 계층 간 데이터 교환을 위한 Java Beans
  - View와 통신하기 위한 클래스
  - DB에서 데이터를 받고 이 데이터를 다시 Service 나 Controller 등으로 넘겨주는 역할
  - 따로 세부적인 로직을 갖고 있지 않은, DB로 부터 받을 데이터들을
    어떤 방식, 타입 등으로 받거나 보낼 것인지 정의 해 놓은 양식
    혹은 순수한 데이터 객체
  - getter/setter 나 View와의 통신을 위한 Presentation Logic 정도의 메서드를 가짐
  - VO(Value Object)라는 DTO와 동일한 개념이지만 ‘read only’ 속성을 가지는 Object도 존재

  - DTO
  ```java
  @Getter
  public class UserDto {
  	public String userid;
  	public String password;

  	public SignInReq(String userid, String password) {
  		this.userid = userid;
  		this.password = password;
  	}
  }
  ```

---

## 3. Domain ( = Entity )

- **domain package**
  - 실제 DB의 테이블과 매칭시키는 클래스

  - @Entity, @Column, @Id 등과 같은 Annotation 사용

  - Entity와 DTO를 분리하는 이유

    - Entity는 DB Layer를 위한 것, DTO는 View Layer를 위한 것

    - Entity는 테이블 매핑 클래스로 변경사항이 생기면,
      Entity 뿐만 아니라 다른 여러 클래스에 영향을 주기 때문에 설계 시에 신중히 만들고
      이후 변경사항이 상대적으로 다소 적은 클래스
    - DTO는 request/response에 대한 부분 혹은 View 관련 Presentation Logic을 가진다.
      상대적으로 자주 변경되는 클래스이기 때문에 이 둘을 분리할 필요가 있다.
    - DTO는 Entity(=Domain) Model을 복사 해 와서,
      Presentation Logic을 추가하거나 DTO 상에서만 필요/불필요 한 필드 멤버를 추가/삭제한 클래스 구조

  - Entity
  ```java
  @Entity
  public class Member {

  	@Id @GeneratedValue(strategy = GenerationType.IDENTITY)
  	private long id;

  	private String name;
  	public long getId() {
  		return id;
  	}

  	public void setId(long id) {
  		this.id = id;
  	}

  	public String getName() {
  		return name;
  	}

  	public void setName(String name) {
  		this.name = name;
  	}
  }
  ```
  ***
  - 참고자료
    [Crow.log](https://velog.io/@linger0310/DDD#dtodata-transfer-object)
