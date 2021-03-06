# Kurento



## Kurento란?

- WebRTC의 사양이 모두 구현된 WebRTC 미디어 서버와 클라이언트 API를 제공하는 패키지로 WebRTC 화상 어플리케이션의 개발을 가능하게하는 오픈 소스



## 🤔미디어 서버를 왜 사용할까?

- 유튜브, 인스타 라이브와 같은 대규모의 서비스에는 한 명의 스트리머와 N명의 시청자가 존재
- 1 : N 스트리밍 또는 다양한 기능들을 추가하기 위해 P2P 방식을 사용해서 개발하기에는 무리

     → Peer 중간에 미디어 서버 필요!

    ![stun](/res/kurento.png)

    ### MCU(Multipoint Control Unit)

    - 다대다 통신에서 여러 미디어 스트림을 하나의 스트림으로 만든 후, 클라이언트에게 제공
    - 서버의 CPU 부하가 SFU에 비해 높은 편
    - SFU에 비해 더 적은 양의 데이터로 미디어 스트림을 받을 수 있다.

### SCU(Selective Forwarding Unit)

- 다대다 통신에서 여러 미디어 스트림을 하나로 만들기 위한 디코딩, 인코딩 작업 없이 클라이언트에게 제공
- 서버의 CPU 부하는 MCU에 비해 낮은 편
- MCU에 비해 더 많은 양의 데이터를 수신