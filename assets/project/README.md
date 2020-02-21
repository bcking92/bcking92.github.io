# Trip Diary : 편리한 여행기록 웹 서비스

[toc]

<br>

### 개요

여행기록을 편하게 작성할 수 있는 방법이 없을까? 사진만 넣어주면 자동으로 여행 일정을 정리해주었으면 좋겠다. 그럼 만들어보자. 사진의 메타정보를 이용해서 내가 다녀온 여행을 간편하지만 이쁘게 포스팅하고 공유할 수 있고 관심있는 사람이나 여행 포스트들을 확인할 수 있는 서비스!!!

<br>

### 팀소개

- 팀장
  - 육성현
- 팀원
  - 김민지
  - 최현빈
  - 조경환
  - 김병철

<br>

### 기술스택

##### 1. `VueJS(VueX, Vuesax, Ant)`

- `VueJS` vs `React`
  - 만드는 규모의 웹앱이 큰 규모가 아니기 때문에 러닝 커브가 낮은 VueJS를 선택했다.

##### 2. `NodeJs(Express, TypeScript, Typeorm, routing-controller, PM2)`

- `SpringBoot` VS `Django` VS `Express`
  - 우리가 구현하려고 하는 서비스는 CSR(Client Side Rendering)기반으로 서버에서는 간단한 데이터를 저장하고 다시 뿌려주는 일 정도밖에 하지 않는다. 이렇게 CPU 사용이 적지만 동시에 여러 connection을 처리해야하는 상황에서 Node는 큰 강점을 발휘한다.
  - 싱글스레드 언어이기 때문에 동기화에 대한 걱정이 없다.
  - Node는 러닝 커브도 높지않다.
  - JSON입력을 클래스로 변환할 필요없이 바로 사용할 수 있다.
  - Node를 사용하면 프론트 팀원과 백엔드 팀원이 서로 코드를 쉽게 읽을 수 있다.
  - 멀티 코어 환경에서는 자원 효율 측면에서 싱글스레드가 단점이 될 수도 있기에 PM2를 이용해서 멀티 프로세싱을 구현하는 방식을 선택했다.

##### 3. `MySQL`

##### 4. `AWS(EC2, RDS, S3)` 

##### 5. `JWT`

- `세션id` VS `JWT`

  - JWT는 저장공간이 따로 필요없으므로 서버 메모리 관리 측면에서 좋다.
  - JWT는 secret key만 있으면 유효성을 검증할 수 있으므로 분산처리시 데이터 공유 문제에대한 걱정이 없다. 

  <br>

### 데이터베이스

![img](https://d2sqqdb3t4xrq5.cloudfront.net/upload/nuboG4d35QJeLoim2/NHU4bndYWXU0SGpwZ3NFaUFfd003YTRMdHd4U0pnV2RtaTIucG5n)

<br>

### 벡엔드 서버 구조

![backend](backend.jpg)

<br>

### 프론트엔드 서버 구조
  