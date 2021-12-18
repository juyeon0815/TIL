# OAuth

---

### 1️⃣ OAuth란?

- 타사의 사이트에 대한 접근 권한을 얻고, 그 권한을 이용하여 개발할 수 있는 환경을 제공하는 프로토콜
- 쉽게 말해, 외부 서비스에서도 인증을 가능하게 하고 그 서비스의 API를 이용하게 해주는 것
- 다른 서비스로 로그인 하기 기능을 구현할때 사용한다면 = 다른 서비스의 회원 정보를 안전하게 사용하기 위한 방법

### 2️⃣ OAuth 참여자

- Resource Server : Client가 제어하고자 하는 자원을 보유하고 있는 서버
    - ex) 네이버, 구글, 페이스북, 트위터
- Resource Owner : 자원의 소유자 = 실제 유저
- Client : Resource Server에 접속해서 정보를 가져오고자 하는 클라이언트 = 웹 어플리케이션

### 3️⃣ 흐름

![stun](/res/oauth1.png)

### ⭐구글을 예로 들어서 설명 (Authorization Code Grant 방식)

- 구글에 나의 `웹 어플리케이션을 등록`하여 Client ID와 Secret Key 생성
    - Client ID와 Secret Key는 Client를 식별하고 신원을 확인하는데 사용
    
    ❓ 나의 웹 어플리케이션을 등록하는 이유는?
    
    - 악의적인 사용자가 xss공격이나 피싱 사이트를 이용해서 redirect_uri를 변경한다면 access token으로 사용자의 정보를 받을 수 있을 것이다. 하지만 웹 어플리케이션을 등록한다면 내가 등록해 놓은 redirect_uri이 아닌 다른 값으로 보냈다면 구글은 이를 수상하다고 여기고 보내주지 않을 것이다.
    
- 구글 아이디로 나의 웹 페이지 회원가입을 진행한다면
  
    ![stun](/res/oauth2.png)
    
    1. 사용자가 구글아이디로 로그인 or 회원가입 진행
    2. 구글계정으로 로그인 성공 시 Authentication code와 함께 Redirect URL로 이동
    3. Client는 Authentication Code와 Clinet Id, Secret Key, Redirect URL 정보를 Resource Server에게 넘겨주어 Access Token 발행 요청
    4. Resource Server는 접근할 수 있는 Access Token, Refresh Token 발행
    5. Client는 Access Token으로 사용자의 정보 접근 가능(email, name 등)
    6. Access Token 만료 시, Refresh Token을 통해 새로 발급
    

### ❓OAuth를 왜 쓸까?

- 편리하다
    - 웹 서비스를 이용하기 위해서는 회원가입 절차가 필요한 경우가 대부분인데, 사이트별 id와 password를 기억하는 것은 매우 귀찮다. 만약 OAuth를 활용한다면 자주 사용하는 서비스의 id와 password만 기억해 놓으면 소셜 로그인을 진행할 수 있기 때문에 간단하다.
- 안전하다
    - 검증되지 않은 App에서 OAuth를 사용해서 로그인을 진행한다면, 유저의 민감한 정보가 App에 노출된 위험이 없고 인증 권한에 대한 허가를 미리 유저에게 구해야하기 때문에 안전하게 사용할 수 있다.

### ❓JWT와 OAuth의 차이는 뭘까?

- JWT와 OAuth는 둘 다 인증 관점에서 비교하여 생각할 수 있겠지만 서로가 추구하는 목적이 다르다.
    - OAuth는 하나의 플랫폼의 권한으로 다양한 플랫폼에서 권항르 행사할 수 있게 해줌으로써 리소스 접근이 가능하게 하는데 목적을 두고 있음
    - JWT는 Cookie, Session을 대신하여 의미있는 문자열 토큰으로써 권한을 행사할 수 있는 토큰의 한 형식임 (로그인 세션이나 주고받는 값이 유효한지 검증할 때 사용)