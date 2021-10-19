# Spring이란?

---

## Spirng이란?

- Java언어 기반의 프레임워크
- Java로 다양한 어플리케이션을 만들기 위한 프로그래밍 틀

### 프레임워크 ❓

- 프로그램 기본 구조(뼈대)
- 원하는 기능 구현에만 집중하여 빠르게 개발할 수 있도록 기본적으로 필요한 기능을 갖추고 있는 것

### 💡스프링(Spring)의 특징

⭐결합도를 낮춰 유연할 개발 가능하게 해준다!

- 제어의 역전(IOC : Inversion of Control)
    - 프로그램의 생명주기에 대한 제어권이 웹 애플리케이션 컨테이너에 있다. (이게 무슨말..)
    - 사용자가 직접 new 연산자를 통해 인스턴스를 생성하고 메서드를 호출하는 일련의 생명주기에 대한 작업들을 스프링에 위임
    
- 의존성 주입(DI)
    - 객체 사이에 필요한 의존 관계에 대해서 스프링 컨테이너가 자동으로 연결해 주는 것
    - DI를 이용하여 빈(Bean) 객체 관리, 스프링 컨테이너에 클래스를 등록하여 스프링이 클래스의 인스턴스를 관리해 준다.
    
    👉🏻스프링 컨테이너에 빈(Bean)을 등록하고 설정하는 방법
    
    1. XML 설정을 통한 DI - applicationContext.xml에서 설정
    2. 어노테이션을 이용한 DI
    
    ```java
    //DI가 없는 예제
    @RestController
    public class Controller{
    	Service service = new Service(); //객체간의 결합도↑
    
    @RequestMappint("/hello")
    public String hello(){
    		return service.helloMessage();
    	}
    }
    ```
    
    ```java
    //DI가 있는 예제
    
    //service
    @Component
    public class Service{
    	public String helloMessage(){
    		return "hello~"
    	}
    }
    
    //controller
    @RestController
    public class Controller{
    	@Autowired
    	Service service;
    
    	@RequestMappint("/hello")
    	public String hello(){
    		return service.helloMessage();
    	}
    
    }
    ```
    
    → 어노테이션으로 Service 객체의 인스턴스를 쉽게 얻을 수 있다. = 결합도↓
    
- 관점 지향 프로그래밍(AOP)
    - 주요 핵심 기능과 핵심 기능 구현을 위한 부가적인 기능(로깅 작업, 데이터베이스 연결 및 트랜잭션 처리, 파일 입출력 등) 구현을 분리하여 각각의 관점별로 묶어서 개발하는 방식

### 왜 스프링 부트가 필요할까❓

- Spring MVC 프레임워크를 사용할 때 applicationContext.xml이외에 다양한 설정을 통해 의존성을 주입해야한다.
- 기본 프로젝트를 셋팅하는데 많은 시간 소요

### 그럼 Spring Boot는 뭐가 다를까❓

- Spring Boot는 따로 설정할 필요 없이 단지 실행만 하면 된다!
- spring-boot-starter-web을 사용하면 종속된 모든 라이브러리를 알맞게 찾아서 가져오기 때문에 종속성이나 호환 버전에 대해 신경 쓸 필요가 없다!

👀 참고

[https://dzone.com/articles/spring-vs-spring-boot](https://dzone.com/articles/spring-vs-spring-boot)

[https://msyu1207.tistory.com/entry/Spring-VS-Spring-Boot-차이점을-알아보자](https://msyu1207.tistory.com/entry/Spring-VS-Spring-Boot-%EC%B0%A8%EC%9D%B4%EC%A0%90%EC%9D%84-%EC%95%8C%EC%95%84%EB%B3%B4%EC%9E%90)