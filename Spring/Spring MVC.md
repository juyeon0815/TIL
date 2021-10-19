# Spring MVC

---

## Spring MVC란?

👉🏻 model, view, controller의 합성어로 소프트웨어 디자인 패턴

- Model : Controller에서 받은 데이터를 저장하는 역할
- View : jsp 파일등과 같이 화면에 시각적으로 표현해주는 역할
- Controller : 사용자의 요청을 받고 응답을 하는 로직을 담당. 접근한 url에 따라 요청사항을 파악하고 그에 맞는 데이터를 model에 의뢰하고 view에 반영해서 사용자에게 보여주는 역할

### 👉🏻Spring MVC 요청흐름

- Request → DispatcherServlet (web.xml) → Controller → Logic처리(service, db접근) → View 전달 → response

---

- DispatcherServlet : 모든 request를 받는 관문. request를 실제로 처리할 Controller에게 클라이언트의 요청을 전달하고, controller가 리턴한 결과값을 View에게 전달하여 알맞은 응답 생성
- Controller : 클라이언트의 요청을 처리한 뒤, Model을 호출하고 그 결과를 DispatcherServlet에게 알려줌
- View :  Controller의 처리결과를 보여울 응답화면 생성

### 👉🏻VO, DTO, DAO란?

- VO(Value Object) : 실제 데이터만 저장하는 클래스
- DTO(Data Transfer Object) : 데이터를 주고 받기 위해 사용하는 클래스
- DAO(Data Access Object) : DB에 접근하여 실제 데이터를 조회/조작하는 클래스 Repository 또는 Mapper에 해당

### 👉🏻MVC Pattern 특징

- 어플리케이션의 확장을 위해 model, view, controller 세 영역으로 분리
- 컴포넌트의 변경이 다른 영역의 컴포턴트에 영향을 미치지 않는다. = 유지보수 용이하다.
- 컴포넌트 간의 결합성이 낮아 프로그램 수정이 용이하다. = 확장성이 뛰어나다.
  
    

장점

- 화면과 비즈니스 로직을 분리해서 작업 가능
- 영역별 개발로 확장성 뛰어남
- 표준화된 코드를 사용하므로 공동작업 용이 및 유지보수성 좋음

단점

- xml를 기반으로하는 프로젝트 설정은 많은 시간 소요
- Tomcat과 같은 WAS 별도 설치

해결책( = Spring Boot)

- 자동설정을 도임하여 DispatcherServlet과 같은 설정 시간 감소
- spring-boot-starter로 외부 도구 사용
- 내장 톰캣 제공하여 별도의 WAS 필요 X

---

## 웹 서버 VS WAS❓

- 웹 서버(Apache) : 클라이언트가 웹 브라우저의 어떠한 페이지 요청을 하면 웹 서버에서 그 요청을 받아 정적 컨텐츠(HTML, CSS 등 즉시 응답가능한 컨텐츠)를 제공하는 서버
- WAS(Tomcat) : 웹 서버 단독으로 처리할 수 없는 데이터베이스의 조회나 다양한 로직 처리가 필요한 동적 컨텐츠를 제공하는 서버

---

### 👉🏻그럼 웹 서버는 동적 컨텐츠를 제공하지 못하나?

- 웹 서버가 동적 컨텐츠 요청을 받으면 WAS에게 해당 요청을 넘겨주고, WAS에어 처리한 결과를 클라이언트에게 전달해주기도 한다!

### 👉🏻 그럼 WAS를 쓰면 되는거 아닌가?

- WAS는 DB조회 및 다양한 로직처리하는 데 집중하기 때문에 단순한 정적 컨텐츠를 웹 서버에 맡겨 기능을 분리시킴으로써 서버 부하 방지!
- 만약 WAS가 정적 컨텐츠 요청까지 처리한다면, 동적 컨텐츠 처리가 지연되면서 수행 속도도 느려질뿐더러 이로 인해 페이지 노출 시간이 지연되는 문제가 발생하여 효율성이 크게 떨어진다.

### 👉🏻 그럼 Apache Tomcat은 다른건가?

- Tomcat에 정적 컨텐츠를 처리하는 기능이 추가되어, Tomcat가 Apache기능을 포함하고 있어 Apache Tomcat이라고 부른다!

👀참고

[https://codechasseur.tistory.com/25](https://codechasseur.tistory.com/25) (웹서버 WAS차이)

[https://minchoi0912.tistory.com/93](https://minchoi0912.tistory.com/93) (Spring MVC)