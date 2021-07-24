# gitignore

---

## 🙄 gitignore이란?

- 프로젝트 작업시 로컬 환경 정보나 빌드 정보등 원격 저장소에 실수로 올라가지 않도록 관리하는 파일



## 🙄 gitignore를 왜 사용할까?

- 원하지 않는 파일이 업로드되는 일 방지
- 충돌로 인한 데이터 손실 방지



## 📔 .gitignore 설정 방법

1. .gitignore 파일 생성

    $ vi .gitignore

    ⇒ 이름 앞에 . 가 붙으면 숨김파일로 생성된다.

    

2. 파일 수정
    - 작성 패턴
        - #로 시작하는 라인 무시
        - /로 시작하면 하위 디렉터리에는 적용❌
        - 디렉터리는 /를 끝에 사용
        - !로 시작하는 패턴의 파일은 무시❌

    EX) # Node artifact files

     node_modules/

     dist/

    
    
3. 수정 후

    git add . → commit → push



## 🏁 확인해보기

1.  .gitignore 파일에 업로드 하지 않을 파일 입력

![stun](/res/gitignore.png)



2. push후 확인해보면!

![stun](res/check.png)

업로드안된거 확인!