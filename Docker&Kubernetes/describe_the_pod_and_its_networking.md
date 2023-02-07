# describe_the_pod_and_its_networking

## VM vs Container vs Pod

virtualization - virtual machine

containerization - container 

kubernetes - pod

atomic unit of scheduling

## what is a pod

k8s에서 생성되고 관리되는 가장 작은 유닛 

application의 하나의 instance만 대표한다 

일반적으로 pods는 stateful이 아니다 

정상 작동하지 않는 pods은 고치는 것이 아니라 교체시킨다 

node 안에 pod 안에 각자의 volume을 가진 containerized app이 존재 

## cloud native function (CNF)

1. CNF 
    
    bare metal에서 돌아가는 microservice 기반의 architecture cloud native function 
    
2. pod in CNF
    
    하나 이상의 컨테이너의 논리적인 집합 
    
    - 하나의 호스트에게 같이 스케줄된다
    - 같은 외부 저장소에 마운트된다
3. 특징 
    1. pod는 하나의 노트에서 실행된다 
    2. pod는 다수의 노드로 뻗어 갈 수 없다 
    3.  replicas라 불리는 다수, 유사한 pods를 deploy(배포) 할 수 있다 
    4. pods는 다른 노드로 migrated(이동) 할 수 없다 (가상 머신과 동일하게)

## Networking: containers in different pods

- 하나의 노드 안의 다른 pod들이 통신하는 방법

같은 호스트 내 모든 컨테이너는 같은 브릿지 (cbr0) 네트워크로 연결되어 있다  

컨테이너 간의 소통은 IP를 사용하여 진행된다 (from pod and required port)

## Networking: containers in the same pods

- 하나의 pod 안의 컨테이너들이 통신하는 방법

동일한 pod에 속한 모든 컨테이너들은 ip 주소를 expose 하고, common network stack을 공유한다 

각 컨테이너의 서비스는 ports를 통해 exposed 된다 (각 컨테이너는 포트 번호가 다르다)

포트는 같은 pod에 있는 컨테이너 사이에는 공유되지 않는다 

같은 pod 안에 있는 컨테이너들은 `localhost:port`를 통해 소통한다


## pods, containers and microservice

### micro-service

application의  분리된 구성요소 

### container

패키징, 배포, 프로세스 실행 등의 방법

배포, 실행에서 사용되는 os 레벨의 가상화 

### pods

compute, 네트워크, 저장 공간 유닛

저장 자원, 유일한 네트워크 식별자로 구분된 반드시 함께 실행되어야 하는 그룹

### node

물리 혹은 가상머신 자원
