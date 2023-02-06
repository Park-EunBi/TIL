# explain_the_k8s_architecture_and_its_building_blocks

- [Node Components](#node-components)
- [Control Plane](#control-plane)
- [control plane components](#control-plane-components)
- [cloud native application](#cloud-native-application)

## Node Components

1. container Runtime Engine
    
    software responsible for running containers (such as docker)
    
2. kube -porxy
    
    forwards network traffic to of from pods 
    
3. kubelet
    
    Agent that moniors container health
    

run on every node 

provide the runtime environment and maintains the pods 

## Control Plane

makes global decisions about the cluster, such as 

- scheduling
- detecting and responding to cluster events
- starting up a new pod

일반적으로는 pods/containers을 보유하지 않음 

노드와 그들의 컴포넌트를 관리함 

## control plane components

1. kube-apiserver 
    
    control plane의 접근을 위해 k8s api를 expose
    
2. kube-scheduler
    
    실행을 위해 새로 생성된 pods를 노드에 할당한다  
    
3. kube-controller-manager 
    
    노드가 down 되는 것을 모니터 하고 응답하거나 
    
    pods의 수를 유지한다 
    
4. cloud manager controller 
    
    cloud provider’s api와의 연결을 허용한다 
    
5. etcd
    
    쿠버네티스의 클러스터 데이터를 위한 backing store로 사용되는 지속가능하고 고사용성의 key-value 저장소
    

## cloud native application

using kubernetes

쿠버네티스를 사용하여 cloud native application을 deploy 하는 방법 

가장 하단에 virtual 혹은 physical muchines이 존재 

그 위에 CaaS(Service as a service)가 구성된다 

그 안에 control plane, node가 설치된다 

node 위에 pod, k8s service, colue native application이 차례로 생성된다
