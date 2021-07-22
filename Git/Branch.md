# Git

---

## 📔Git-flow

- 서로간의 약속



### 🙄로컬 저장소, 원격 저장소의 개념

- 로컬 저장소
    - 내 PC에 파일이 저장되는 개인 전용 저장소
- 원격 저장소
    - 파일이 원격 저장소 전용 서버에서 관리되며 여러 사람이 함께 공유하기 위한 저장소
    
    

### Git-flow 브랜치

- master : 제품으로 출시될 수 있는 브랜치
- develop : 다음 출시 버전을 개발하는 브랜치
- feature : 기능을 개발하는 브랜치
- hotfix : 출시 버전에서 발생한 버그를 수정하는 브랜치
- release : 이번 출시 버전을 준비하는 브랜치



### 📕동작순서

 1. feature/login , feature/join 등과 같이 기능 구현이 필요할 경우 feature 브랜치 생성해 회원가입 기능, 로그인 기능 등을 구현한다.

1. 기능 구현이 완료되면 develop 브랜치에 합친다. (Merge)
2. 모든 기능이 완료되면 develop 브랜치를 release 브랜치로 만든 뒤, 테스트를 진행하면서 보완점을 보완하고 버그를 픽스한다.
3. 완료되면 release 브랜치를 master 브랜치와 develop 브랜치로 보낸다
    1. release 브랜치를 master / develop 에 보내는 이유?

        : meger가 된 후에는 자동으로 브랜치가 삭제되기 때문에 merge후 혹여나 중요한 수정사항이 생길 수 있으니, develop 브랜치에 백업을 해두는 것

4. master 브랜치에서는 배포 진행
5. 배포 후 버그 발견 시, hotfix 브랜치를  만들어 수정후 배포 진행
    1. hotfix 브랜치는 master 브랜치에 기반하여 생성
    2. 수정 후에는 master/develop 브랜치에 merge되며, master에 업데이트된 버전 번호 태깅
    
    

### 🌳branch

- 브랜치 생성

    $ git branch [ 브랜치 이름 ]

- 브랜치 목록보기

    $ git branch -a

- 해당 브랜치로 이동하기

    $ git checkout [ 브랜치 이름 ]

- 브랜치 삭제하기 (로컬스토리지)

    $ git branch -D [ 브랜치 이름 ]

- 브랜치 삭제하기 (원격스토리지)

    $ git push origin —delete [ 브랜치 이름 ]

- 브랜치 merge

    $ git checkout [ 저장될 브랜치 이름]

    $ git merge [ merge할 브랜치 이름 ]

    ex ) feature/login 브랜치에서 로그인 기능 구현 완료 후, develop 브랜치에 merge

    $ git check out develop

    $ git merge feature/login
    
    

### 📌주의점

1. master 브랜치에서 작업 x
2. feature → master로 바로 업데이트 x , develop 브랜치를 부모 브랜치로 삼아 develop 브랜치에 merge



### ❓ git bash에서 txt 파일 수정하는 방법

- vi [ name ].txt
- txt파일 열렸으면 i누르고 txt파일 수정
- esc → shift + ; → wq



### ❓ pull과 fetch의 차이

- git pull : 서로 연결된 원격 저장소의 최신 내용을 로컬 저장소로 가져오면서 병합

- git fetch : 로컬 저장소와 원격 저장소의 변경 사항이 다를 때 이를 대조하고 git merge 명령어와 함께 최신 데이터를 반영하거나 충돌 문제 등 해결

    자동 병합 x → 직접 병합하는 과정 거쳐야한다.



### ❓ switch와 checkout의 차이

- checkout → switch , restore 로 대체

    이유? checkout 명령어가 가진 기능이 너무 많기때문에 switch, restore로 기능 세분화

- git switch : 브랜치를 변경

- git restore : 워킹 트리의 파일 복원

    ex ) 파일의 수정 내용을 복원하려면 $ git checkout — [README.md](http://readme.md) → $ git restore README.md



### ❓ Merge와 Rebase의 차이

- 공통점 : 한 브랜치에서 다른 브랜치로 합치기
- 실행결과는 같지만 커밋 히스토리가 다르다.
- merge : 각각의 브랜치 + 공통 부모의 커밋을 이용한 3-way merge를 수행해 새로운 커밋 생성
- rebase : 공통 부모가 되는 base를 다른 브랜치의 커밋 지점으로 바꿈



### ❓ 브랜치안에 하위 브랜치를 만들 수 있나?

- 만들 수 없다!!

  

### ❓ 다른브랜치에서 pull 할 수 있나? master 에서만 pull할 수 있나?

- 서로 다른 브랜치에서 pull을 하게되면 merge를 하는것과 동일
- $ git checkout [저장할 브랜치명]

    $ git checkout [가져올 브랜치명] — [가져올 파일이름]

    ex ) develop 브랜치에 있는 test.txt 파일 feature 브랜치로 pull 하기

    $ git checkout feature

    $ git checkout develop — test.txt

    📌 한개의 파일을 가져온 적 있다면 복수의 파일 가져올 경우 커밋하고 다른 파일 가져오기