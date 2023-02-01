# term

- [용어 정리](#-----)
  * [container](#container)
  * [container image](#container-image)
  * [container runtime](#container-runtime)
  * [kubernetes](#kubernetes)
  * [container **Orchestration**](#container---orchestration--)
  * [Helm](#helm)
  * [kubernetes POD](#kubernetes-pod)
- [배포](#--)
  * [전통적인 배포](#-------)
  * [가상 머신 기반 배포](#-----------)
  * [컨테이너 기반 배포](#----------)
- [참고자료](#----)

### container

application을 실행할 수 있는 환경까지 감싸 어디든 실행할 수 있게 만든 것 

### container image

컨테이너 환경을 묶어서 배포한 것 

### container runtime

컨테이너를 사용할 때 필요한 도구 

컨테이너를 쉽게 내려받고, 공유, 구동할 수 있게 하는 것 

ex) docker 

→ 도커로 만든건 규격화 되어 있어서 도커 말고 다른 컨테이너 런타임들도 도커로 만든 것을 사용할 수 있다

### kubernetes

컨테이너 런타임으로 컨테이너를 다루는 도구 

### container **Orchestration**

쿠버네티스가 하는 일 

여러 서버 (노드)에 컨테이너 분산

문제 발생 컨테이너 교체

컨테이너 버전 관리, 환경 설정 등 

### Helm

쿠버네티스 패키지 매니저 

(python의 pip와 동일한 기능)

### kubernetes POD

리눅스 컨테이너를 하나 이상 모아둔 것 

쿠버네티스 application의 최소 단위

같은 pod에 속한 컨테이너들을 컴퓨팅 리소스를 공유한다 

컨테이너는 전통적인 방식처럼 하나의 os위에서 동작하지만 

각 컨테이너가 실행되면서 간섭되지 않도록 장벽을 친다 

→ cpu, memory 자원 또한 독립적으로 사용될 수 있도록 할당되고 관리된다

⇒ os kernel을 공유하는 가상화

## 배포

### 전통적인 배포

com 1개, os 1개

자원을 여러 프로그램이 나눠 씀 

### 가상 머신 기반 배포

com 1개, 가상 머신 여러 개 (각각의 os 설치)

각 가상머신이 완전히 격리됨

→ 개별적으로 자원 할당 

### 컨테이너 기반 배포

컴퓨터 형태에 영향을 받지 않음, os 1개

실행 환경은 격리되지만 os는 공유됨

## 참고자료

[쿠버네티스 알아보기 1편: 쿠버네티스와 컨테이너, 도커에 대한 기본 개념](https://www.samsungsds.com/kr/insights/220222_kubernetes1.html)
