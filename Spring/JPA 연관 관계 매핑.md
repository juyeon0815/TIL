# JPA

# 📋연관 관계 정의 규칙

- 방향 : 단방향, 양방향
- 연관 관계의 주인
- 다중성 : 일대일(1:1), 일대다(1:N), 다대일(N:1), 다대다(N:M)



## ↔️ 단방향, 양방향

- 두 객체 사이에 하나의 객체만 참조용 필드를 갖고 참조 → 단방향 관계

- 두 객체 모두가 각각의 참조용 필드를 갖고 참조 → 양방향 관계

    양방향 관계는 ↔️ 가 아닌, 단방향 참조를 각각 가지고 서로 참조하는 것
    
    

### 🤜🏻양방향 매핑시 주의할 점

- 연관 관계의 주인은 연관 관계를 갖는 두 객체 사이에서 조회, 저장, 수정, 삭제를 할 수 있지만, 연관 관계의 주인이 아닌 경우에는 조회만 가능

- mappedBy 속성을 사용해서 주인 지정

    ⇒ 외래 키가 있는 곳이 연관 관계의 주인!!!!!!!!!!!
    
    

## 👩🏻‍🌾 연관 관계의 주인

- 두 객체중 제어의 권한(저장, 수정, 삭제)을 갖는 실질적인 관계가 어떤 것인지 파악
- 연관 관계의 주인은 저장,수정,삭제,조회를 할 수 있지만, 연관 관계의 주인이 아닌경우에는 조회만 가능



## ✏️ 다중성

1. 일대일(1:1)
    - 어느 곳이든 외래키를 가질 수 있다.
    - 외래키 한개만 있어도 양쪽 조회 가능
        1. 주 테이블

            주 테이블만 확인해도 대상 테이블과의 연관 관계 확인 가능

        2. 대상 테이블

            테이블 관계가 일대일에서 일대다로 변경되었을 경우에 테이불 구조 유지
            
            
    
1. 일대다(1:N) : 실무에서는 일대다(1:N) 단방향은 거의 쓰지 ❌
    - N 테이블에 외래키 존재
    - 1이 연관관계의 주인
    - 반대편 테이블의 외래 키를  관리하는 특이한 구조

    
    
2. 다대일(N:1) : JPA에서 가장 많이 사용
    - 다(N) 쪽에서 외래키 관리

    
    
3. 다대다(N:M) 
    - 되도록이면 사용하지말자!

       왜❓

    다대다로 만들었을 경우, 개발하다가 그에 따른 데이터가 추가될 수도 있는데 다대다로 매핑되어 있을 경우에는 매핑 정보만 넣을 수 있고, 다른 추가 정보는 넣을 수 없기 때문!

      🤔 그럼 어떻게해야할까..?

    - 다대다(N:M)을 일대다(1:N). 다대일(N:1)로 만들어주기!
    
    

![stun](/res/entity.png)



- User

```java
@Entity
@Getter
@Setter
public class User {
    @Id
    @GeneratedValue(strategy = GenerationType.IDENTITY)
    int id;

		String userName;

    @OneToMany (mappedBy ="user")
    @OnDelete(action = OnDeleteAction.CASCADE)
    List<UserHashtag> userHashtag = new ArrayList<>();
}
```



- UserHashtag

```java
@Entity
@Getter
@Setter
public class UserHashtag extends BaseEntity {

    @ManyToOne
    @JoinColumn(name="userId")
    User user;

    @ManyToOne
    @JoinColumn(name="hashtagId")
    Hashtag hashtag;

}
```



- Hashtag

```java
@Entity
@Getter
@Setter
public class Hashtag{
		@Id
    @GeneratedValue(strategy = GenerationType.IDENTITY)
    int id;

    String tagName;

    @OneToMany(mappedBy ="hashtag")
    List<UserHashtag> userHashtags = new ArrayList<>();
}
```



## 👉🏻 어노테이션 정리

- @Entity : 데이터베이스의 테이블과 일대일로 매칭되는 객체 단위
- @id : Primary Key
- @Table : 데이터베이스상의 실제 테이블 명칭을 지정

    - 지정하지않을 경우, Entity 클래스 이름 그대로 테이블 명칭 지정

    - 테이블 이름을 명시적으로 작성하는 것이 관례

- @Column : 데이터베이스의 테이블에 있는 컬럼과 동이하게 1:1 매칭
- @GeneratedValue : Primary key의 기본값을 자동으로 생성할때 사용
- @ManyToOne : 다대일 관계를 나타내는 매핑 정보
- @JoinColumn : 외래 키 매핑 시 사용