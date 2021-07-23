# JPA

---

- Java Persistence API ( 자바 ORM 기술에 대한 API 표준 명세)
- ORM을 사용하기 위한 인터페이스를 모아둔 것



## ORM이란?

- Object-relational mapping ( 객체 관계 매핑 )
- 객체는 객체대로 설계 / 관계형 데이터베이스는 관계형 데이터베이스대로 설계 ⇒ ORM 프레임워크가 중간에서 매핑



## JPA 동작과정

![STUN](/res/operationProcess.png)

JPA를 사용하지 않았던 경우 👉🏻 JAVA애플리케이션이 JDBC API를 사용해 DB와 통신

JPA를 사용한 경우 👉🏻 JPA를 통해 JDBC API를 사용하여 SQL을 통해 DB와 통신하고 그 결과를 반환



### - 저장

![STUN](/res/save.png)

📌 동작과정 (👂🏻 JPA가  상속관계 등 알아서 해결 )

1. DB에 넣고싶은 Member 정보를 MemberDAO에 담기
2. JPA 메소드 PERSIST 호출
3.  JPA가 Member Entity분석 후 SQL 생성
4. JDBC API를 사용하여 DB에 INSERT QUERY 전달



### - 조회

![stun](/res/inquiry.png)

📌 동작과정

1. 객체를 분석해 적절한 SELECT SQL 생성
2. JDBC API를 사용해 SQL 전달
3.  DB에서 반환된 결과를 ResultSet 매핑을 이용해 객체로 만들어서 반환



## 🙄JPA를 사용해야하는 이유?

- 생산성 ( CRUD )

     - 저장 : DB에 저장할 때, jap.persist(member)를 통해 데이터를 넘겨주면, db query가 자동으로 만들어져 넘어간다.  = query를 짤 필요가없다! 호출만해서 사용하면 끝!
     - 조회 : jpa.find(memberId)를 통해 객체만 넘기면 알아서 조회해준다
     - 수정 : member.setName("수정할이름") 를 통해 수정가능
     - 삭제 : jpa.remove(member) 
     
     
     
- 유지보수 : JPA 필드만 추가하면 SQL은 알아서 JPA가 처리

     - SQL문을 고칠 필요X -> 알아서 처리O

     

- JPA와 패러다임의 불일치 해결

     - 상속 

     ![stun](/res/inheritance.png)

     1. 저장 : jpa.persist (Album);
         1. 객체 분해 ( Album 객체는 Item 속성을 모두 가진다)
         2. 각각 INSERT 쿼리를 두 번 날린다.

             ​	INSERT INTO ITEM ...

             ​	INSERT INTO ALBUM ...

             
     2. 조회 : Album album = jpa.find(Album.class, albumId);

         - Item과 Album Join해서 결과 반환

         

      - 연관관계 저장 

     member.setTeam(team);

     jpa.persist(member);

     👉🏻 member에서 team의 PK값을 꺼내 외래키에 자동으로 셋팅

     

      - 객체 그래프 탐색

     Member member = jpa.find(Member.class, memberId);

     Team team = member.getTeam();

     👉🏻 jpa를 통해 member 정보를 가져와 member.getTeam()를 하면 해당 정보 가져오기
