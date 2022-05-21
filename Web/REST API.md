# REST API

---

## API란?

- Application Programming Interface
- 응용 프로그램에서 사용할 수 있도록, 운영체제나 프로그래밍 언어가 제공하는 기능을 제어할 수 있게 만든 인터페이스

---

### 👉🏻 OPEN API는 뭘까?

- 프로그래밍에서 사용할 수 있는 개방되어 있느 상태의 인터페이스
- NAVER, KAKAO 등 포털 서비스 사이트 등 다양한 데이터를 외부 응용 프로그램에서 사용할 수 있도록 OPEN API를 제공

## REST란?

- Representational State Transfer의 약어로 하나의 URL은 하나의 고유한 리소스를 대표하도록 설계된다는 개념에 전송방식을 결합해서 원하는 작업 지정
  
    ![stun](/res/rest.png)
    
- HTTP URI를 통해 제어할 자원을 명시하고 HTTP Method를 통해 해당 자원을 제어하는 명령을 내리는 방식의 아키텍처

---

- HTTP Method
    - POST : 리소스 생성
    - GET : 리소스 조회
    - PUT : 리소스 수정
    - DELETE : 리소스 삭제
    

### 👉🏻GET / POST 차이

- GET방식 : 클라이언트에서 서버로 어떤 리소스로부터 필요한 정보를 요청하기 위해 사용하는 메서드 EX) 게시판 게시물 조회
    - 데이터 URL주소 끝에 파라미터로 쿼리 스트링을 포함하여 전송
    - 요청 길이에 제한있다.
    - 파라미터에 붙여서 전달하기 때문에 보안에 취약하다.
    - 멱등이다.
    
- POST방식 : 클라이언트에서 서버로 리소스를 생성하거나 업데이트하기 위해 데이터를 보낼 때 사용하는 메서드 EX) 게시판 글 작성
    - 데이터 HTTP 메시지 BODY부분에 담아서 전송
    - 요청 길이에 제한이 없다.
    - BODY에 담아서 보내기 때문에 데이터 노출되지 않아 보안에 강함
    - 멱등이 아니다.
    
    ### 멱등이 뭐야❓
    
    - 연산을 여러 번 적용하더라도 결과가 달라지지 않는 성질
    - 즉, GET은 리소스를 조회만하기 때문에 여러 번 요청하더라도 응답은 똑같을 것이다. 하지만 POST는 리소스를 새로 생성하거나 업데이트할 때 사용되기 때문에 멱등이 아니라고 볼 수 있다.
    

### 👉🏻Swagger란?

- 간단한 설정으로 프로젝트의 API 목록을 웹에서 확인 및 테스트 할 수 있게 해주는 라이브러리