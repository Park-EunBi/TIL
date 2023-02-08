# describe_the_deployment_and_statefulSet_in_kubernetes

# deployments

다수의 stateless application replicas들을 고사용성을 위해 돌린다 

pods의 새로운 상태를 선언한다 

이전 상태로 수정할 수 있다 

더 많은 로드를 용이하게 하기 위해 scale up 한다 

PodTemplateSpec의 다수의 수정 사항을 적용하기 위해 멈추고, 새로운 rollout을 위해 다시 시작한다 

더 이상 사용하지 않는 replicaset을 지운다 

# statefulSet

application의 stateful을 관리하는 데 사용되는 워크로드 api 오브젝트 

deployment와 유사하게 statefulset 또한 개발 컨테이너 spec을 기반으로 pods를 관리한다 

차이점은 statefulset은 stateful applications를 위해 각각의 pods에 대해 sticky한 정체성을  유지한다는 것

요구되는 최적의 application

- stable, unique network identifiers
- stable, persistent storage

[스테이트풀셋](https://kubernetes.io/ko/docs/concepts/workloads/controllers/statefulset/)

[Stateful / Stateless Application](https://m.blog.naver.com/4u_olion/222007062998)
