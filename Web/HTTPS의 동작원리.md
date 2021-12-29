# HTTPS의 동작원리

---

### 1️⃣ HTTPS (Hypertext Transfer Protocol Secure)

- HTTP의 보안 버전

![stun](/res/https1.png)

- TCP 위에 SSL/TLS 층을 추가하여 암호화, 인증, 무결성 보장을 통해 더 안전하게 만들어주는 프로토콜



### 2️⃣ HTTP 동작과정

- 대칭키와 공개키(비대칭키) 방식을 전부 사용하는 하이브리드 방식

- 데이터 전송을 위해 대칭키 방식을 사용하며 대칭키를 안전하게 전달하기 위해 공개키 방식을 사용
  
    ![stun](/res/https2.png)
    
    1. Client Hello
        - 브라우저마다 지원하는 암호화 알고리즘과 TLS버전이 다르므로 해당 정보와 난수 값을 생성하여 전송
    2. Server Hello
        - 사용할 TLS버전, 사용할 암호화 알고리즘, 난수값 전송
    3. Certificate
        - CA로부터 발급받은 인증서 전송
    4. Server Key Exchange
        - 키 교환에 필요한 정보 제공
        - 필요하지 않으면 과정 생략 가능
    5. Certificate Request
        - 서버가 클라이언트에게 인증서를 요구하는 단계 (요청하지 않을 수도 있음)
    6. Server Hello Done
    7. Client Key Exchange, Change Cipher Sepc
        - pre-master-key 전송 (1,2단계에서 생성한 난수를 조합하여 생성 → 대칭키로 사용, 전송은 공개키 방식 사용)
    8. Change Cipher Spec
        - 클라이언트로부터 전송받은 pre-master-key를 복호화 한 뒤, master-key로 승격 후 보안 파라미터를 적용하거나 변경될때 보내는 알림
        
        
    
    위 과정을 통해 공개키 방식으로 대칭키를 안전하게 설정하여 데이터를 송/수신
    
    
    
    ⭐ 참고 ⭐
    
    [https://mysterico.tistory.com/30](https://mysterico.tistory.com/30)