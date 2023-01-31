# NR_leg_setup

- [배경지식](#----)
  * [용어정리](#----)
  * [eNB와 gNB의 특징](#enb--gnb----)
  * [5g 서비스 이동 경로](#5g----------)
- [UE가 5G를 사용하고 release 하는 과정](#ue--5g-------release------)
  * [1. UE power-on](#1-ue-power-on)
  * [2. NAS UE가 cell에 attach](#2-nas-ue--cell--attach)
  * [3. B1 event](#3-b1-event)
  * [4. NR Leg Setup](#4-nr-leg-setup)
  * [5. data 전달](#5-data---)
  * [6. connection release](#6-connection-release)
  * [7. UE power-off](#7-ue-power-off)
  * [8. (mct test 진행시) mct 자원 반납](#8--mct-test------mct------)
- [MCT test](#mct-test)
  * [참고 자료](#-----)

## 배경지식

### 용어정리

UE(user equipment): 단말기 

eNB(eNodeB): 4G base band

gNB(gNodeB):5G base band 

NSA(not standard alone): 혼자 작동할 수 없는 gNB, eNB가 반드시 필요

UE Capability: RRC message that UE sents to Network, NSA, UE 등의 세팅 값이 저장되어 있음 

[4G | ShareTechnote](https://www.sharetechnote.com/html/Handbook_LTE_UE_Capability.html)

RRC(Radio Resource Control)

UE와 network를 연결하는 과정중 거치는 중요한 단계 

hand-over: 단말기를 이동할 때 다른 기지국으로 연결되는 것 

MeNB: master eNB

SgNB: secondary gNB

GTE: 실제 통신 기기 대신 test 할 수 있는 시뮬레이터, eNB, gNB, UE등의 역할을 한다 

MCT test: Multi component test 

PM: 알고싶은 사건을 event로 만들어서 통계 등에 사용하는 것 

### eNB와 gNB의 특징

1. network로 연결되어 있다 
2. master (eNB) - slave (gNB) 구조
3. UE와 eNB는 주파수를 매개로 data가 이동한다 
4. UE에 따라서 SA(stand alone), NSA가 결정된다 
    
    eNB와 network 모두가 gNB를 지원해야만 gNB가 가능하다 
    

### 5g 서비스 이동 경로

![1](https://user-images.githubusercontent.com/87464975/215729668-c8ee9d97-4d87-4c9c-b2f0-f7a87d1ae91e.png)

5g가 필요한 서비스가 있다면 

eNB를 거쳐 gNB 사용

NSA라면  eNB를 거쳐야 한다

---

## UE가 5G를 사용하고 release 하는 과정

1. UE power-on
2. NSA UE가 cell에 attach
3. B1 event 발생 
4. NR Leg Setup 
5. data 전달 
6. connection release 
7. UE power-off 
8. (mct test 진행시) mct 자원 반납 

### 1. UE power-on

UE가 사용 가능한 상태로 전환된 상태 

### 2. NAS UE가 cell에 attach

UE를 사용가능하도록 cell에 attach 

UE와 eNB는 주파수를 매개로 data가 이동된다 

`**RRC connection Request`** 

UE가 attach 되었는지 확인하는 메시지 

→ ack가 오면 연결되어 사용가능하다는 메시지 

MCT test에서는 power on function

![Untitled](https://user-images.githubusercontent.com/87464975/215728878-f3d99905-f46f-4319-8a55-31d7e2c071ff.png)

### 3. B1 event

![Untitled2](https://user-images.githubusercontent.com/87464975/215729099-c795790e-b093-47a2-9995-940c0041f791.png)

NR cell (5G cell)의 중심으로 가까워지면서

LTE cell 의 줌심으로 멀어짐 

(다른 LTE cell의 중심으로 가까워진다고 하더라도 NR cell에 가까워진다고 판단해야 한다)

### 4. NR Leg Setup

eNB와 gNB를 연결할 다리(x2)를 만들어야 함 

이게 바로 NR Leg Setup

(NR cell은 secondary라서 반드시 eNB와  gNB 사이의 연결이 있어야 한다)

⇒ B1event → NR leg setup → x2 연결 

`**SgNB Addational Request**`

MeNB와 SgNB와의 leg setup을 맺기 위해 보내는 메시지 

SgNB가 ACK 보내면 그 안에 id 값이 같이 보내짐 

이걸로 MeNB는 UE id 튜플 쌍을 생성

(UE id는 유일하지만 eNB, gNB가 UE id를 저장하는 방식이 다름, 그래서 같은 UE를 나타낸 것이라고 튜플로 묶어 정리하는 것) 

cf) 통신할 때에는 X2ap UE id 사용 

### 5. data 전달

연결된 다리로 data를 전달한다 → 5g 서비스 이용 가능 

### 6. connection release

전원을 끄거나, 빠른 속도로 이탈하는 상황등이 발생할 때 

연결을 release 하고 자원 회수 

`ENDC x2 partial request`

트리거를 트리거 하는 msg

반납할 UE list가 있을 때 UE를 반납하기 위해 보내는 msg 

eNB는 cell 단위로 UE를 release 한다 

`RRC connection release`

UE에 할당된 모든 리소스를 제거하고, 사이클을 제거하는 msg

### 7. UE power-off

### 8. (mct test 진행시) mct 자원 반납

테스트에 사용된 자원 반납 

---

## MCT test

목표: 해당 과정이 잘 작동하는지 확인

방법: msg들이 잘 오고가는지 peeking, pm 기능 작동 확인 

### 참고 자료

1. SgNB Addtional Request  

[5G NR cell rejects SgNB Addition Request issue and root cause](https://www.rfwireless-world.com/5G/5G-NR-cell-rejects-SgNB-Addition-Request-issue-and-root-cause.html)

![s](https://user-images.githubusercontent.com/87464975/215729272-41b23b95-c493-416a-b98b-072e213b8883.png)

2. 용어 정리 

[5G 기지국의 기술 표준 구조 (NSA)](https://wiseworld.tistory.com/entry/5G-%EA%B8%B0%EC%A7%80%EA%B5%AD%EC%9D%98-%EA%B8%B0%EC%88%A0-%ED%91%9C%EC%A4%80-%EA%B5%AC%EC%A1%B0-NSA)

[[5G] 5G 네트워크 구조 정리 (5G RAN과 5G Core)](https://jb-story.tistory.com/346)

[5G 네트워크 아키텍처란? - Shunlongwei Co. Ltd](https://www.shunlongwei.com/ko/what-is-5g-network-architecture/)
